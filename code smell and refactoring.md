# Code smell and refactoring

[https://martinfowler.com/books/refactoring.html]()

## **重构定义**
> 对软件内部结构的一种调整，目的是在不改变【软件之可察行为】前提下提高其可理解性，降低其修改成本。

## **基本原则**：
> 清晰、简洁、模块尽可能小、易于重用而不是拷贝、模块之间依赖小

## **代码异味**
> **Code Smell**中文译名一般为“代码异味”，或“代码味道”，它是提示代码中某个地方存在错误的一个暗示，开发人员可以通过这种smell（异味）在代码中追捕到问题。

在计算机编程社区中，code smell代表了任何标志着事物变坏的征兆。它常常标志代码应该被refactored或者全部的设计都应该被reviewed。这个短语出现在 WardsWiki上，它是被Kent Beck杜撰出来的。在refactoring兴起之后，这个短语的使用率骤增。

###22种代码的坏味道

### 1.Duplicated Code(重复的代码)
代码重复几乎是最常见的异味了。他也是Refactoring 的主要目标之一。代码重复往往来自于copy-and-paste 的编程风格。与他相对应OAOO 是一个好系统的重要标志。
**用到的重构方法**   : 
> Extract Method(提炼函数), Pull Up Method(函数上移), From Template Method(塑造模板函数), Substitute Algorithm(替换算法), Extract Class(提炼类);

### 2.Long Method(过长方法)
它是传统结构化的“遗毒”。一个方法应当具有自我独立的意图，不要把几个意图放在一起，特别注意大类和长方法。
**用到的重构方法**   : 
>  Extract Method(提炼函数), Replace Temp with Query(以查询取代临时变量), Introduce Parameter Object(引入参数对象), Preserve Whole Object(保持对象完整), Decompose Conditional(分解条件表达式);

### 3.Large Class(过大类)

大类就是你把太多的责任交给了一个类。这里的规则是One Class One。
**用到的重构方法**   : 
>  Extract Class(提炼类), Extract Subclass(提炼子类), Extract Interface(提炼接口), Duplicate Observed Data(复制被监视的数据);

### 4.Long Parameter List(过长参数列)

**用到的重构方法**   : 
>  Replace Parameter with Method(以函数取代参数), Preserve Whole Object(保持对象完整), Introduce Parameter Object(引入参数对象);

### 5.Divergent Change(发散式变化)
一个类里面的内容变化率不同。某些状态一个小时变一次，某些则几个月一年才变一次；某些状态因为这方面的原因发生变化，而另一些则因为其他方面的原因变一 次。面向对象的抽象就是把相对不变的和相对变化相隔离。把问题变化的一方面和另一方面相隔离。这使得这些相对不变的可以重用。问题变化的每个方面都可以单 独重用。这种相异变化的共存使得重用非常困难。
**用到的重构方法**   : 
>  Extract Class(提炼类);

### 6. 霰弹式修改 (Shotgun Surgery)
这正好和上面相反。对系统一个地方的改变涉及到其他许多地方的相关改变。这些变化率和变化内容相似的状态和行为通常应当放在同一个类中。
**用到的重构方法**   : 
>  Move Method(搬移函数), Move Field(搬移字段), Inline Class(内联化类);

### 7. 依恋情结 (Feature Envy)

对象的目的就是封装状态以及与这些状态紧密相关的行为。如果一个类的方法频繁用get 方法存取其他类的状态进行计算，那么你要考虑把行为移到涉及状态数目最多的那个类。
**用到的重构方法**   : 
>  Move Method(搬移函数)，Extract Method(提炼函数)

### 8.数据泥团(Data Clumps)
某些数据通常像孩子一样成群玩耍：一起出现在很多类的成员变量中，一起出现在许多方法的参数中……，这些数据或许应该自己独立形成对象。
**用到的重构方法**   : 
>  Extract Class(提炼类), Introduce Parameter Object(引入参数对象),Preserve Whole Object(保持对象完整)

### 9.Primitive Obsession(基本型别偏执)
面向对象的新手通常习惯使用几个原始类型的数据来表示一个概念。譬如对于范围，他们会使用两个数字。对于Money，他们会用一个浮点数来表示。因为你没 有使用对象来表达问题中存在的概念，这使得代码变的难以理解，解决问题的难度大大增加。好的习惯是扩充语言所能提供原始类型，用小对象来表示范围、金额、 转化率、邮政编码等等。
**用到的重构方法**   : 
>  Replace Data Value with Object(), Replace Type Code with Class(), Replace Type Code with Subclass(), Replace Type Code with State/Strategy(), Extract Class, Introduce Parameter Object, Replace Array with Object

### 10.Switch Statements(switch惊悚现身)
基于常量的开关语句是OO 的大敌，你应当把他变为子类、state 或strategy。
**用到的重构方法**   : 
>  Move Method(搬移函数)，Extract Method(提炼函数), Replace Type Code with Subclasses, Replace Type Code with State/Strategy, Replace Conditional with Polymorphism, Replace Parameter with Explicit Methods, Introduce Null Object

### 11.Parallel Inheritance Hierarchies(平等继承体系)

并行的继承层次是shotgun surgery 的特殊情况。因为当你改变一个层次中的某一个类时，你必须同时改变另外一个层次的并行子类。
**用到的重构方法**   : 
>  Move Method, Move Field

### 12.Lazy Class(冗赘类)
一个干活不多的类。类的维护需要额外的开销，如果一个类承担了太少的责任，应当消除它。
**用到的重构方法**   : 
>  Collapse Hierarchy, Inline Class

### 13.Speculative Generality(夸夸其谈未来性)
一个类实现了从未用到的功能和通用性。通常这样的类或方法唯一的用户是test case。不要犹豫，删除它。
**用到的重构方法**   : 
>  Collapse Hierarchy, Inline Class, Remove Parameter, Rename Method

### 14.Temporary Field(令人迷惑的暂时字段) 
一个对象的属性可能只在某些情况下才有意义。这样的代码将难以理解。专门建立一个对象来持有这样的孤儿属性，把只和他相关的行为移到该类。最常见的是一个特定的算法需要某些只有该算法才有用的变量。

**用到的重构方法**   : 
>  Extract Class, Introduce Null Object

### 15.Message Chains(过度耦合的消息链)
消息链发生于当一个客户向一个对象要求另一个对象，然后客户又向这另一对象要求另一个对象，再向这另一个对象要求另一个对象，如此如此。这时，你需要隐藏分派。
**用到的重构方法**   : 
>  Hide Delegate, Extract Method

### 16.Middle Man(中间转手人)
对象的基本特性之一就是封装，而你经常会通过分派去实现封装。但是这一步不能走得太远，如果你发现一个类接口的一大半方法都在做分派，你可能需要移去这个中间人。
**用到的重构方法**   : 
>  Remove Middle Man, Inline Method, Replace Delegation with Inheritance

### 17.Inappropriate Intimacy(狎昵关系)
某些类相互之间太亲密，它们花费了太多的时间去砖研别人的私有部分。对人类而言，我们也许不应该太假正经，但我们应当让自己的类严格遵守禁欲主义。
**用到的重构方法**   : 
>  Move Method, Move Field, Change Bidirectional Association to Unidirectional, Replace Inheritance with Delegation, Extract Class, Hide Delegate

### 18.Alternative Classes with Different Interfaces(异曲同工的类)
做相同事情的方法有不同的函数signature，一致把它们往类层次上移，直至协议一致。
**用到的重构方法**   : 
>  Rename Method, Extract Superclass

### 19.Incomplete Library Class(不完美的程序库类)
要建立一个好的类库非常困难。我们大量的程序工作都基于类库实现。然而，如此广泛而又相异的目标对库构建者提出了苛刻的要求。库构建者也不是万能的。有时 候我们会发现库类无法实现我们需要的功能。而直接对库类的修改有非常困难。这时候就需要用各种手段进行Refactoring。
**用到的重构方法**   : 
>  Move Method, Introduce Foreign Method, Introduce Local Extension

### 20.Data Class(纯稚的数据类)
对象包括状态和行为。如果一个类只有状态没有行为，那么肯定有什么地方出问题了。
**用到的重构方法**   : 
>  Encapsulate Field, Encapsulate Collection, Remove Setting Method, Move Method, Extract Method, Hide Method

### 21.Refused Bequest(被拒绝的遗赠)
超类传下来很多行为和状态，而子类只是用了其中的很小一部分。这通常意味着你的类层次有问题。
**用到的重构方法**   : 
>  Push Down Method, Push Down Field, Replace Inheritance with Delegation

### 22.Comments(过多的注释)
经常觉得要写很多注释表示你的代码难以理解。如果这种感觉太多，表示你需要Refactoring。
**用到的重构方法**   : 
>  Extract Method, Rename Method, Introduce Assertion



## 重构列表
Refactoring:Improving the Design of Existing Code

1. Add parameter(添加参数)
2. Change bidirectional association to unidirectional(将双向关联改为单项)
3. Change reference to value (将引用对象改为实值对象)
4. Change unidirectional assocation to bidirectional(将单项关联改为双向)
5. Change value to reference (将实值对象改为引用对象)
6. Collapse hierachy(折叠继承体系)
7. Consolidate conditional expression(合并条件式)
8. Consolidate duplicate conditional fragments(合并重复的条件判断)
9. Convert procedural design to objects(将过程化设计转化为对象设计)
10. Decompose conditional (分解条件式)
11. Duplicate observed data(复制“被监视数据”)
12. Encapsulate collection (封装群集)
13. Encapsulate downcast(封装“向下转型”动作)
14. Encapsulate field（封装值域）
15. Extract class（提炼类）
16. Extract hierarchy （提炼继承体系）
17. Extract interface（提炼接口）
18. Extract method（提炼函数）
19. Extract subclass（提炼子类）
20. Extract superclass（提炼超类）
21. Form template method（塑造模板函数）
22. Hide delegate（隐藏委托关系）
23. Hide method（隐藏函数）
24. Inline class （将类内联化）
25. Inline method（将函数内联化）
26. Inline Temp（将临时变量内联化）
27. Introduce assertion（引入断言）
28. Introduce explaining ariable（引入解释性变量）
29. Introduce foreign method（引入外加函数）
30. Introduce local extension（引入本地扩展）
31. Introduce null object（引入Null对象）
32. Introduce prrameter object（引入参数对象）
33. Move field （搬移值域）
34. Move method(搬移函数)
35. Parameterize method（令函数携带参数）
36. Preserve whole object（保持对象完整）
37. Pull up constructor body（构造函数本体上移）
38. Pull up field（值域上拉）
39. Pull up method（函数上拉）
40. Pull down field（值域下降）
41. Pull down method（函数下移）
42. Remove assignments to parameters（移除函数的赋值动作）
43. Remove control flag（移除控制标记）
44. Remove middleman（移除中间人）
45. Remove parameter（移除参数）
46. Remove setting method（移除设置函数）
47. Rename method（重新命名函数）
48. Replace array with object（以对象取代数组）
49. Replace conditionalwith polymorphism（以多态取代条件式）
50. Replace constructor with factory method（以工厂方法取代构造函数）
51. Replace data value with object(以对象取代数据值)
52. Replace delegation with inheritance（以继承取代委托）
53. Replace error code with exception（以异常取代错误码）
54. Replace exception with test（以测试取代异常）
55. Replace inheritance with delegation（以委托取代继承）
56. Replace magic number with symbolic constant（以字面常量代替魔法数字）
57. Replace method with method object（以函数对象取代函数）
58. Replace nested conditional with guard clauses（以卫语句取代条件式）
59. Replace parameter with method（以函数取代参数）
60. Replace parameter with explicit methods（以明确函数取代参数）
61. Replace record with data class（以数据类取代记录）
62. Replace subclass with field（以值域取代子类）
63. Replace temp with query（以查询取代临时变量）
64. Replace type code with class（以类取代型别码）
65. Replace type code with state/strategy（以state/strategy取代性别码）
66. Replace type code with subclass（以子类取代型别码）
67. Self encapsulate field（自封装值域）
68. Separate domain from presentation (将领域和表述/显示分开)
69. Separate query with modifier (将查询函数和修改函数分离)
70. Split tempory variable(剖解临时变量)
71. Substitue algorithm(替换你的算法)
72. Tease appart inheritance(梳理并分解继承体系)


* 代码异味：[https://sourcemaking.com/refactoring/smells]()
* 代码异味参考：[http://xp.c2.com/CodeSmell.html]()
* 重构列表：[https://refactoring.com/catalog/]()