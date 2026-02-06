#StandardEvaluationContext
使用 `StandardEvaluationContext`（SpEL）实现“外置规则”，核心思路是**将 SpEL 表达式字符串存储在外部**（如数据库、配置中心、文件），并在运行时读取该字符串，利用 SpEL 的 `ExpressionParser` 进行动态解析和执行。

相比于硬编码在 Java 类中，这种方式实现了规则与代码的解耦。

以下是使用 SpEL 实现外置规则引擎的完整实现方案：

### 1. 核心架构设计

- **规则存储层**：外部数据源（数据库表、Redis、Nacos/Apollo 配置中心）存储规则字符串。
- **规则解析层**：`ExpressionParser` 负责将字符串编译成 `Expression` 对象。
- **上下文执行层**：`StandardEvaluationContext` 负责承载业务数据（变量），并执行规则判断或计算。

### 2. 代码实现步骤

#### 第一步：定义规则存储模型

假设你在数据库中有一张 `rule_config` 表，关键字段如下：

表格

|字段名|说明|示例值|
|---|---|---|
|`rule_key`|规则标识|`discount_rule_v1`|
|`rule_expr`|**外置的 SpEL 表达式 (核心)**|`#user.level == 'VIP' && #order.amount > 1000`|
|`status`|状态|`ENABLED`|

#### 第二步：创建业务数据对象

java

编辑

```
1// 用户对象
2@Data
3public class User {
4    private String level; // 等级
5    private int score;    // 积分
6}
7
8// 订单对象
9@Data
10public class Order {
11    private BigDecimal amount; // 金额
12    private String type;       // 类型
13}
```

#### 第三步：编写规则引擎执行器 (核心)

这个类负责从外部获取规则字符串，并执行它。

编辑

```java
1import org.springframework.expression.Expression;
2import org.springframework.expression.ExpressionParser;
3import org.springframework.expression.spel.standard.SpelExpressionParser;
4import org.springframework.expression.spel.support.StandardEvaluationContext;
5
6import java.math.BigDecimal;
7import java.util.Map;
8
9public class SpelRuleEngine {
10
11    // 1. 定义解析器 (全局单例即可)
12    private final ExpressionParser parser = new SpelExpressionParser();
13
14    /**
15     * 执行规则
16     * @param spelExpression 从数据库或配置中心获取的表达式字符串
17     * @param variables 业务数据 (Key-Value 形式)
18     * @return 规则执行结果 (Boolean 或 计算值)
19     */
20    public Object executeRule(String spelExpression, Map<String, Object> variables) {
21        
22        // 2. 创建上下文
23        StandardEvaluationContext context = new StandardEvaluationContext();
24        
25        // 3. 注入变量 (将外部传入的数据放入上下文中)
26        // 例如：variables.put("user", userObj); variables.put("order", orderObj);
27        context.setVariables(variables);
28
29        // 4. 解析并执行表达式
30        // 编译模式可选：SpelCompilerMode.OFF, IMMEDIATE, MIXED (高性能场景建议 MIXED)
31        Expression expression = parser.parseExpression(spelExpression);
32        
33        // 5. 执行并返回结果
34        // 如果是判断规则，返回 Boolean；如果是计算规则，返回 Number 等
35        return expression.getValue(context);
36    }
37
38    // --- 测试方法 ---
39    public static void main(String[] args) {
40        SpelRuleEngine engine = new SpelRuleEngine();
41
42        // 模拟从数据库查询出的规则表达式 (这就是"外置"的规则)
43        String ruleFromDB = "#user.level == 'VIP' && #order.amount > 1000";
44
45        // 模拟业务数据
46        User user = new User();
47        user.setLevel("VIP");
48
49        Order order = new Order();
50        order.setAmount(new BigDecimal("1500"));
51
52        // 准备变量上下文
53        Map<String, Object> vars = Map.of(
54            "user", user,
55            "order", order
56        );
57
58        // 执行
59        Object result = engine.executeRule(ruleFromDB, vars);
60        System.out.println("规则执行结果: " + result); // 输出: true
61    }
62}
```

### 3. 高级特性：外置方法调用 (黑白名单/工具类)

如果你的规则需要调用 Java 方法（例如：`isInBlackList(#user.id)`），可以通过注册静态方法或 Bean 来实现。

编辑

```java
1// 工具类
2public class RuleUtils {
3    public static boolean isHighRiskArea(String areaCode) {
4        // 模拟查询数据库或缓存
5        return "RISK_001".equals(areaCode);
6    }
7}
8
9// 在初始化上下文时注册
10StandardEvaluationContext context = new StandardEvaluationContext();
11
12// 注册静态类，别名为 'util'
13context.registerFunction("isHighRisk", 
14    RuleUtils.class.getDeclaredMethod("isHighRiskArea", String.class));
15
16// 此时你的外置规则字符串可以写成：
17String complexRule = "#user.age > 18 && @util.isHighRisk(#user.area)";
```

### 4. 性能优化建议

1. **缓存 Expression 对象**：  
    SpEL 的解析（`parseExpression`）是有成本的。因为你的规则字符串（`rule_expr`）通常变化不频繁，建议使用 `ConcurrentHashMap` 缓存编译后的 `Expression` 对象，不要每次执行都重新解析。

    ```java
    
    1private final Map<String, Expression> expressionCache = new ConcurrentHashMap<>();
    2Expression expression = expressionCache.computeIfAbsent(spelExpression, parser::parseExpression);
    ```
    
2. **开启编译模式**：  
    对于高频调用的规则，设置 SpEL 的编译模式为 `MIXED` 或 `IMMEDIATE`，它会将表达式编译成字节码，性能提升显著。

    ```java
    1SpelParserConfiguration config = new SpelParserConfiguration(SpelCompilerMode.MIXED, null);
    2ExpressionParser parser = new SpelExpressionParser(config);
    ```
    
3. **变量命名规范**：  
    建议统一使用 `#` 前缀（如 `#user`），这符合 SpEL 的标准规范，也方便开发人员编写规则。
    

### 总结

使用 `StandardEvaluationContext` 做外置规则，本质就是**字符串模板引擎**。

- **外置**：把 `#user.level == 'VIP'` 存在数据库里。
- **注入**：把 Java 对象（User, Order）塞进 `StandardEvaluationContext`。
- **执行**：用 `Expression.getValue(context)` 动态计算真假或值。

这种方式非常适合 Spring Boot 项目，因为它天然支持 Spring 的各种类型转换和对象访问。