---
title: Design Patterns
date: 2022-08-07 21:04:20
---

### 前言

最近花了点读了《敏捷软件开发》这本书，关于这本书，我基本上是随便看看，了解有什么知识，也就在代码部分（具体示例方面）花了些功夫。尽管知道了解了这些知识，但是在工程上，没写个1w行以上的代码还是难以融会贯通。毕竟理论和工程是不一样的，工程实现理论至少是两个数量级以上的难度。不过通过画简单的UML图和短小的代码是可以快速认识到是什么，用来做什么，这样就足够了。

### 《敏捷软件开发》阅读经验

这本书还是一本很好的书，对于了解敏捷开发，设计模式是足够的，同时也有足够多的源代码可以读。我读的一版是《敏捷软件开发：原则、模式与实践》c++版本的，不过里面也有java，虽然我的主语言是c#，但是也是阅读起来也不会太困难。这本书中文版虽然是在03年出版的，但是在现在对于我这种未入行业的小白也是十分有启发的。
根据我这次阅读的经验，我推荐第I部分（也就是1-6章）还有第II部分的第7章**粗读**，对原则和设计模式之类的进行**通读**，18，19章的薪水支付实践进行**细读**

### 什么是设计模式

设计模式是软件设计中常见问题的典型解决方案。 它们就像能根据需求进行调整的预制蓝图，可用于解决代码中反复出现的设计问题。不过设计模式的出现基本上是为了解决 **“设计的臭味”** ——僵化性(Rigidity)，脆弱性(Fragility)，牢固性(Immobility)，粘滞性(Viscosity)，不必要的复杂性(Needless Complexity)，不必要的重复(Needless Repetition)，以及晦涩性(Opacity)

- **僵化性**：很难对系统改动，因为每次改动都会使其他地方改动
- **脆弱性**：对系统的改动会导致其他的地方出现问题
- **牢固性**：设计中包含对其它系统有用的部分，但是把这部分抽离出来成本太高
- **粘滞性**：做新的改动时，保持系统设计的方法比破坏设计的方法更难使用
- **不必要的复杂性**：包含当前没有用的组成部分，可能会变得混乱
- **不必要的重复**：包含重复的结构，原本可以用单一的抽象进行统一
- **晦涩性**：难以阅读、理解

#### 设计模式的描述常常包含以下内容

- **意图(Problem)** 部分简单描述问题和解决方案。
- **动机(Solution)** 部分将进一步解释问题并说明模式会如何提供解决方案。
- **结构(Structure)** 部分展示模式的每个部分和它们之间的关系。

#### 学习设计模式的好处以及一些问题

- 现在常常说的23种设计模式是经过实践验证的解决方案。了解这些设计模式对于阅读源代码十分有用。
- 同时方便交流，只要知晓模式以及名称的原理，就可以用一个设计模式的名字来互相沟通这里该怎么写

同时设计模式也一些问题，设计模式有一些是为了弥补语言本身的缺陷，有些语言有方便的语法，基本上一句话就可以代表一种设计模式。

“如果你只有一把铁锤， 那么任何东西看上去都像是钉子。” 这点是最重要的，对于初学者会带来一定困扰，学习某个模式之后，他们会在所有地方使用该模式，即便是在较为简单的代码中也使用这种模式。所以说初学者学来帮助自己阅读源码就绰绰有余了。

### UML类图

在学习设计模式之前，我们得先学会如何读UML图。虽然UML图有很多种，但是基本上只要会读UML类图，就可以胜任大部分的工作。

#### UML类方框

UML类图中基本上就三种普通类，抽象类和接口。都用矩形框表示，第一层是类名称，第二层是成员变量，第三层是类的方法。

- **"+"** 表示 public
- **"-"** 表示 private
- **"#"** 表示 protected

抽象类的类名以及抽象方法都用**斜体**，接口会在第一层加上一个 **<< interface >>** ，其他并没有什么不同

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220807220610.png)
![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220807221329.png)
![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220807221347.png)

#### UML类图中的关系

下面一张图如果可能的话应该在《c++ prime plus》中看过，可以很快理解是什么意思，我们基本上只要记得关系对应的箭头就可以了。不过不知道也没关系，我们可以快速过一遍，了解足矣。
![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220807221552.png)

##### 实现关系

简单来说就是类实现接口，由类指向接口
![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220807222154.png)

##### 泛化关系

指对象之间的继承关系，由子类指向父类
![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220807222354.png)

##### 关联关系

指这个对象在内部引用了另一个对象，关联关系内部又为依赖关联、聚合关联和组合关联三种类型

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220807222649.png)

##### 依赖关系

指A使用了B，但是A和B并没什么关系，就可以认为是依赖关系

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220807223108.png)

##### 聚合关系

指A拥有B，B可以属于多种A

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220807223430.png)

##### 组合关系

指A包括B，同生同灭

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220807223521.png)

#### UML类图小结

大概稍微看一下就行了，我认为看英文(is a那些)更容易理解关系是什么意思，虽然关联关系还可再分，不过基本上不搞那么详细。毕竟UML类图是为了前期快速构思类的关系的，基本上我们只用前三种关系——**实现关系、泛化关系，关联关系**

### 面向对象设计的一些原则

在了解设计模式之前，我们需要了解一些原则，这也是使用设计模式的目的之一。

#### 单一职责原则(SRP-Single Responsibility Principle)

当一个类承担的职责过多，就等于把这些职责耦合在了一起，一个职责变化的时候，可能就容易导致其他职责的变化。假设一个类既可以链接管理，又可以进行数据通信，在数据通信方面由于客户需求不断变化，可能在数据通信方面不断修改导致链接管理修改起来也很麻烦，这时就应该分离这两个职责，让两个职责分别置于不同的类中。

#### 开放-封闭原则(OCP-The Open-Closed Principle)

指的是在一个类中新加入的扩展的功能并不需要修改原有的功能。比如说绘制图案，原本只能绘制正方形和圆形，如果加入三角形，那在绘制图案的时候只需添加三角形这个类而不修改其他类。

#### Liskov替换原则(LSP-Liskov Substitution Principle)

违反LSP原则必然违反OCP原则，任何基类可以出现的地方，子类一定可以出现，即在使用时子类可以替换掉基类但是功能不受影响

#### 依赖导致原则(DIP-Dependency Inversion Principle)

- 高层模块不应该依赖于底层模块，二者都应该依赖于抽象
- 抽象不应该依赖于细节，细节应该依赖于抽象

高层模块即实践模块，比如main函数，修改了main函数的实现方式却不改变底层模块类的代码变化

#### 接口隔离原则(ISP-Interface Segregation Principle)

建立单一接口，不要建立臃肿庞大的接口。再通俗一点讲：接口尽量细化，同时接口中的方法尽量少。跟SRP差不多

### 设计模式介绍

设计模式可以根据其意图来分类。主要分为三种类别

- **创建型模式(Creational Patterns)** 提供创建对象的机制， 增加已有代码的灵活性和可复用性
- **结构型模式(Structural Patterns)** 介绍如何将对象和类组装成较大的结构， 并同时保持结构的灵活和高效
- **行为模式(Behavioral Patterns)** 负责对象间的高效沟通和职责委派

### 创建型模式(Creational Patterns)

#### Factory Method(工厂模式)

工厂模式是一种创建型设计模式，其在父类中提供一个创建对象的方法， 允许子类决定实例化对象的类型。

##### 问题

假设你正在开发一款物流管理应用。 最初版本只能处理卡车运输， 因此大部分代码都在位于名为**卡车**的类中。一段时间后， 这款应用变得极受欢迎。 你每天都能收到十几次来自海运公司的请求， 希望应用能够支持海上物流功能。这可是个好消息。 但是代码问题该如何处理呢？ 目前， 大部分代码都与 卡车类相关。 在程序中添加 轮船类需要修改全部代码。 更糟糕的是， 如果你以后需要在程序中支持另外一种运输方式， 很可能需要再次对这些代码进行大幅修改。

##### 解决方案

工厂方法模式建议使用特殊的工厂方法代替对于对象构造函数的直接调用（即使用 new运算符）。不用担心， 对象仍将通过new运算符创建，只是该运算符改在工厂方法中调用罢了。工厂方法返回的对象通常被称作 “产品”。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220808133543.png)

这样子，我们可以在子类中重写工厂方法。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220808134434.png)

举例来说，**RoadLogically**类的工厂方法也就是**createTransport()**返回的便是**Truck**对象，而**SeaLogistics**返回的便是**Ship**对象。

调用工厂方法的代码 （通常被称为客户端代码） 无需了解不同子类返回实际对象之间的差别。 客户端将所有产品视为抽象的运输。 客户端知道所有运输对象都提供交付方法，但是并不关心其具体实现方式。

##### 工厂方法模式结构

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220808164835.png)

由图可以看到这个结构被分为了两部分，一个Creator部分，一个Product部分，Creator部分负责创建，同时提供SomeOperation()进行操作，而SomeOperation()内部是获得具体物体的接口，并且做出具体实现。

1.**产品(Product)** 将会对接口进行声明。 对于所有由创建者及其子类构建的对象， 这些接口都是通用的。

2.**具体产品(Con­crete Prod­ucts)** 是产品接口的不同实现。

3.**创建者(Cre­ator)** 类声明返回产品对象的工厂方法。 该方法的返回对象类型必须与产品接口相匹配。

你可以将工厂方法声明为抽象方法，强制要求每个子类以不同方式实现该方法.或者，你也可以在基础工厂方法中返回默认产品类型。

注意，尽管它的名字是创建者，但它最主要的职责并不是创建产品。一般来说，创建者类包含一些与产品相关的核心业务逻辑。工厂方法将这些逻辑处理从具体产品类中分离出来.打个比方，大型软件开发公司拥有程序员培训部门。但是，这些公司的主要工作还是编写代码，而非生产程序员。

4.**具体创建者(Con­crete Cre­ators)** 将会重写基础工厂方法，使其返回不同类型的产品。

注意，并不一定每次调用工厂方法都会创建新的实例。工厂方法也可以返回缓存、对象池或其他来源的已有对象。

##### 伪代码

根据上图，我们可以快速的做出一个基于运输例子的伪代码(并不是很伪)，如果有新的种类，比如说飞机，那么修改就很容易了，并不需要修改原来的代码，只需要多写一个**AirLogistics类**继承**Logistics类**，写一个**Plane**继承**Transport接口**，甚至连父类的Logistics都不用动，这很好的践行了SRP和OCP原则。

```csharp
//Logisitic抽象类，也就是Creator
public abstract class Logisitic
{
    //CreateTransport也就是工厂方法(FactoryMethod)
    public abstract Transport CreateTransport();

    public void planDelivery()
    {
        Transport t = CreateTransport();
        t.Deliver();
    }
}
public class RoadLogistics : Logisitic
{
    public overrride Transport CreateTransport()
    {
        //返回的是产品类，而不是本尊
        return new Truck();
    }
}
public class SeaLogistics : Logisitic
{
    public overrride Transport CreateTransport()
    {
        return new Ship();
    }
}
//Transport接口，也就是Product
public interface Transport
{
    void Deliver();
}
class Truck : Transport
{
    public void Deliver() 
    {
        //....
    }
}
class Ship : Transport
{
    public void Deliver() 
    {
        //....
    }
}
```

##### 适合工厂模式的地方

- 当你在编写代码的过程中，如果无法预知对象确切类别及其依赖关系时，可使用工厂方法。
- 如果你希望用户能扩展你软件库或框架的内部组件，可使用工厂方法。
- 如果你希望复用现有对象来节省系统资源，而不是每次都重新创建对象，可使用工厂方法。

##### 工厂模式的优缺点

**优点**：

- 你可以避免创建者和具体产品之间的紧密耦合。
- 符合SRP
- 符合OCP
  

**缺点**：

- 应用工厂方法模式需要引入许多新的子类，代码可能会因此变得更复杂。最好的情况是将该模式引入创建者类的现有层次结构中。简单来说，就是在工作初期使用**工厂模式**（比较简单，而且容易通过子类修改),但代码复杂时会演化成其他模式

#### Abstract Factory(抽象工厂模式)

抽象工厂模式是一种创建型设计模式， 它能创建一系列相关的对象， 而无需指定其具体类。

##### 问题

假设你正在开发一款家具商店模拟器。你的代码中包括一些类，用于表示：
1.一系列相关产品，例如 椅子Chair、沙发Sofa和咖啡桌Cof­fee­Table。
2.系列产品的不同变体。例如，你可以使用现代Mod­ern、维多利亚Vic­to­ri­an、​装饰风艺术Art­Deco等风格生成椅子、沙发和咖啡桌。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220808150223.png)

你需要设法单独生成每件家具对象，这样才能确保其风格一致。如果顾客收到的家具风格不一样，他们可不会开心。
此外，你也不希望在添加新产品或新风格时修改已有代码。家具供应商对于产品目录的更新非常频繁，你不会想在每次更新时都去修改核心代码的。

##### 解决方案

首先， 抽象工厂模式建议为系列中的**每件产品**明确声明接口（例如椅子、沙发或咖啡桌）。然后，确保所有产品变体都继承这些接口。例如，所有风格的椅子都实现椅子接口；所有风格的咖啡桌都实现咖啡桌接口，以此类推。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220808150715.png)

接下来，我们需要声明抽象工厂——包含系列中所有产品构造方法的接口。例如cre­ate­Chair创建椅子、​cre­ate­Sofa创建沙发和cre­ate­Cof­fee­Table创建咖啡桌.这些方法必须返回抽象产品类型，即我们之前抽取的那些接口：椅子,沙发和咖啡桌等等。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220808150835.png)

那么该如何处理产品变体呢？对于系列产品的每个变体，我们都将基于抽象工厂接口创建不同的工厂类。每个工厂类都只能返回特定类别的产品，例如，​现代家具工厂Mod­ern­Fur­ni­ture­Fac­to­ry只能创建现代椅子Mod­ern­Chair、现代沙发Mod­ern­Sofa和现代咖啡桌Mod­ern­Cof­fee­Table对象。

客户端代码可以通过相应的抽象接口调用工厂和产品类。 你无需修改实际客户端代码， 就能更改传递给客户端的工厂类， 也能更改客户端代码接收的产品变体。

##### 抽象工厂模式结构

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220808151005.png)

1.**抽象产品(Abstract Prod­uct)** 为构成系列产品的一组不同但相关的产品声明接口。

2.**具体产品(Con­crete Prod­uct)** 是抽象产品的多种不同类型实现。所有变体 （维多利亚/现代）都必须实现相应的抽象产品 （椅子/沙发）。

3.**抽象工厂(Abstract Fac­to­ry)** 接口声明了一组创建各种抽象产品的方法。

4.**具体工厂(Con­crete Fac­to­ry)** 实现抽象工厂的构建方法。每个具体工厂都对应特定产品变体，且仅创建此种产品变体。

5.尽管具体工厂会对具体产品进行初始化，其构建方法签名必须返回相应的抽象产品。这样，使用工厂类的客户端代码就不会与工厂创建的特定产品变体耦合。**客户端 (Client)** 只需通过抽象接口调用工厂和产品对象，就能与任何具体工厂/产品变体交互。

##### 伪代码

同样是根据抽象工厂模式结构的图，我们快速的写一个基于家具抽象工厂的不是那么伪的伪代码

```csharp
//随便写一下代码就会很多，所以这里只写出了一部分代码
//抽象工厂接口
public interface FurnitureFactory
{
    //创建椅子
    Chair CreateChair();

    //创建咖啡桌
    CoffeTable CreateCoffeeTable();

    //创建沙发
    Sofa CreateSofa();
}
public class VictorianFurnitureFactory : FurnitureFactory
{
    public Chair CreateChair()
    {
        return new VictorianChair();
    }

    public CoffeTable CreateCoffeeTable()
    {
        return new VictorianCoffeeTable();
    }

    public Sofa CreateSofa()
    {
        return new VictorianSofa();
    }
}
public class ModernFurnitureFactory : FurnitureFactory
{
    public Chair CreateChair()
    {
        return new ModernChair();
    }

    public CoffeTable CreateCoffeeTable()
    {
        return new ModenCoffeeTable();
    }

    public Sofa CreateSofa()
    {
        return new ModernSofa();
    }
}

//抽象产品 Chair类
public interface Chair
{
    void HasLegs();

    void SitOn();
}

public class VictorianChair : Chair
{
    public void HasLegs()
    {
        //...
    }
    public void SitOn()
    {
        //...
    }
}

public class ModernChair : Chair
{
    public void HasLegs()
    {
        //...
    }
    public void SitOn()
    {
        //...
    }
}

//抽象产品 CoffeeTable类
public interface CoffeeTable
{
    void HasLegs();
}

public class VictorianCoffeeTable : CoffeeTable
{
    public void HasLegs()
    {
        //...
    }
}
public class ModernCoffeeTable : CoffeeTable
{
    public void HasLegs()
    {
        //...
    }
}

//客户端调用抽象工厂代码
public class Client
{
    // - factory:AbstractFactory
    private FurnitureFactory factory;

    public Client(FurnitureFactory factory)
    {
        this.factory = factory;
    }

    public void SomeOperation()
    {
        Chair chair = factory.CreateChair();
        //...
    }
}
```

##### 适合抽象工厂模式的地方

- 如果代码需要与多个不同系列的相关产品交互，但是由于无法提前获取相关信息，或者出于对未来扩展性的考虑，你不希望代码基于产品的具体类进行构建，在这种情况下，你可以使用抽象工厂

##### 抽象工厂模式的优缺点

**优点**:

- 你可以确保同一工厂生成的产品相互匹配
- 你可以避免客户端和具体产品代码的耦合
- 符合SRP
- 符合OCP

**缺点**:

- 由于采用该模式需要向应用中引入众多接口和类， 代码可能会比之前更加复杂。

#### Builder(生成器模式)

生成器模式是一种创建型设计模式，使你能够分步骤创建复杂对象。该模式允许你使用相同的创建代码生成不同类型和形式的对象。

##### 问题

假设有这样一个复杂对象，在对其进行构造时需要对诸多成员变量和嵌套对象进行繁复的初始化工作。这些初始化代码通常深藏于一个包含众多参数且让人基本看不懂的构造函数中；甚至还有更糟糕的情况，那就是这些代码散落在客户端代码的多个位置。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220808163211.png)

最简单的方法是扩展房屋基类，然后创建一系列涵盖所有参数组合的子类。但最终你将面对相当数量的子类。任何新增的参数（例如门廊类型）都会让这个层次结构更加复杂。

另一种方法则无需生成子类。你可以在房屋基类中创建一个包括所有可能参数的超级构造函数，并用它来控制房屋对象。这种方法确实可以避免生成子类，但它却会造成另外一个问题。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220808163441.png)

通常情况下， 绝大部分的参数都没有使用， 这使得对于构造函数的调用十分不简洁。 例如， 只有很少的房子有游泳池， 因此与游泳池相关的参数十之八九是毫无用处的。

##### 解决方案

生成器模式建议将对象构造代码从产品类中抽取出来，并将其放在一个名为生成器的独立对象中。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220808164126.png)

该模式会将对象构造过程**划分为一组步骤**，比如build­Walls创建墙壁和build­Door创建房门创建房门等。每次创建对象时，你都需要通过生成器对象执行一系列步骤。重点在于你无需调用所有步骤，而只需调用创建特定对象配置所需的那些步骤即可。

当你需要创建**不同形式的产品**时，其中的一些构造步骤可能需要不同的实现。例如，木屋的房门可能需要使用木头制造，而城堡的房门则必须使用石头制造。在这种情况下，你可以创建多个不同的生成器，用不同方式实现一组相同的创建步骤。然后你就可以在创建过程中使用这些生成器（例如按顺序调用多个构造步骤）来生成不同类型的对象。

**主管(Director)** :
你可以进一步将用于创建产品的一系列生成器步骤调用抽取成为单独的主管类。主管类可定义创建步骤的执行顺序，而生成器则提供这些步骤的实现。
严格来说，你的程序中并不一定需要主管类。客户端代码可直接以特定顺序调用创建步骤。不过，主管类中非常适合放入各种例行构造流程，以便在程序中反复使用。
此外，对于客户端代码来说，主管类完全隐藏了产品构造细节。客户端只需要将一个生成器与主管类关联，然后使用主管类来构造产品，就能从生成器处获得构造结果了。

##### 生成器模式结构

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220808164617.png)

1.**生成器(Builder)** 接口声明在所有类型生成器中通用的产品构造步骤。

2.**具体生成器(Con­crete Builders)** 提供构造过程的不同实现。具体生成器也可以构造不遵循通用接口的产品。

3.**产品(Prod­ucts)** 是最终生成的对象。由不同生成器构造的产品无需属于同一类层次结构或接口。

4.**主管(Direc­tor)** 类定义调用构造步骤的顺序，这样你就可以创建和复用特定的产品配置。

5.**客户端(Client)** 必须将某个生成器对象与主管类关联。一般情况下，你只需通过主管类构造函数的参数进行一次性关联即可。此后主管类就能使用生成器对象完成后续所有的构造任务。但在客户端将生成器对象传递给主管类制造方法时还有另一种方式。在这种情况下，你在使用主管类生产产品时每次都可以使用不同的生成器。

##### 伪代码

感觉上面的例子并不是很直接，所以我们下面有一个关于生成器模式的例子演示了你可以如何复用相同的对象构造代码来生成不同类型的产品——例如汽车（Car）——及其相应的使用手册（Man­u­al）。
生成器模式可以很方便的写出**实现同类产品但是实现步骤不同**，它会将一个的制造过程分为**一系列步骤**，用Director类在生成不同产品的时候你可以根据不同需求在同类产品选择相应的步骤，比如Car有很多种，在Builder我们有建造Car的所有步骤，但是根据需求只需要使用一些步骤。也就是说，在相应的Builder类中的方法，我们尽量的**详细**，这样在Director中我们能够建造更多类型的产品。
仍然是写一个并不是很伪的伪代码。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220808165345.png)

```csharp
//只有当产品较为复杂且需要详细配置时，使用生成器模式才有意义
//生成器接口声明了创建产品不同对象的方法

//Product类
//一辆车有很多种类，SUV，小轿车等等
public class Car
{
    //...
}
//Product类
public class Manual
{
    //...
}
public interface Builder
{
    void Reset();

    void SetSeats();

    void setEngine();

    //...
    
}
public class CarBuilder : Builder
{
    private Car car = new Car();

    public CarBuilder()
    {
        this.Reset();
    }

    public void Reset()
    {
        this.car = new Car();
    }

    public void SetSeats();

    //...

    //具体生成器需要自行提供获取结果的方法。这是因为不同类型的生成器可能
    // 会创建不遵循相同接口的、完全不同的产品。所以也就无法在生成器接口中
    // 声明这些方法（至少在静态类型的编程语言中是这样的）。
    //通常在生成器实例将结果返回给客户端后，它们应该做好生成另一个产品的准备
    public Car getResult()
    {
        Car result = this.car;

        this.Reset();

        return result;
    }
}

public class CarManualBuilder : Builder
{
    private Manual manual = new Manual();
    public CarManualBuilder()
    {
        this.Reset();
    }

    public void Reset()
    {
        this.manual = new Manual();
    }

    public void SetSeats();

    //...

    public Manual getResult()
    {
        Manual result = this.manual;

        this.Reset();

        return result;
    }
}
//主管类只负责按照特定顺序执行生成步骤
//由于客户端可以直接控制生成器，所以严格意义上来说主管类并不是必需的。
public class Director
{
    private Builder _builder;

    public Builder builder
    {
        set{ _builder = value;}
    }

    public void MakeSUV(Builder builder)
    {
        this._builder.Reset();
        this._builder.setSeat(...);
        //...
    }
    public void MakeSportCar(Builder builder)
    {
        this._builder.Reset();
        this._builder.setSeat(...);
        //...
    } 
}
//客户端类
public class Client
{
    Director director = new Director();

    CarBuilder builder = new CarBuilder();

    director.MakeSportsCar(builder);

    Car car = builder.getResult();

    CarManualBuilder builder = new CarManualBuilder();
    director.MakeSportsCar(builder);

    Manual manual = builder.GetResult();
}
```

##### 适合生成器模式的地方

- 使用生成器模式可避免 **“重叠构造函数 (tele­scop­ing con­struc­tor)”** 的出现。即下列代码

```csharp
class Pizza {
    Pizza(int size) { ... }
    Pizza(int size, boolean cheese) { ... }
    Pizza(int size, boolean cheese, boolean pepperoni) { ... }
}
```

- 当你希望使用代码**创建不同形式的产品** （例如石头或木头房屋） 时，可使用生成器模式。
- 使用生成器构造组合树或其他复杂对象。生成器模式让你能分步骤构造产品。你可以延迟执行某些步骤而不会影响最终产品。你甚至可以递归调用这些步骤，这在创建对象树时非常方便。**生成器在执行制造步骤时，不能对外发布未完成的产品**。这可以避免客户端代码获取到不完整结果对象的情况。

##### 生成器模式的优缺点

**优点** :

- 你可以分步创建对象，暂缓创建步骤或递归运行创建步骤。
- 生成不同形式的产品时，你可以复用相同的制造代码。
- 符合SRP

**缺点** :

- 由于该模式需要新增多个类， 因此代码整体复杂程度会有所增加。

#### Prototype(原型模式)

原型模式是一种创建型设计模式，使你能够复制已有对象，而又无需使代码依赖它们所属的类。(即当你需要一个相同的类，但是重新设置参数很繁琐，原型模式能让你很快地创造一个新的除了名字不一样其他一摸一样的变量)

##### 问题

如果你有一个对象，并希望生成与其完全相同的一个复制品，你该如何实现呢？首先，你必须新建一个属于相同类的对象。然后，你必须遍历原始对象的所有成员变量，并将成员变量值复制到新对象中。但有个小问题。并非所有对象都能通过这种方式进行复制，因为有些对象可能拥有私有成员变量，它们在对象本身以外是不可见的。

直接复制还有另外一个问题。因为你必须知道对象所属的类才能创建复制品，所以代码必须依赖该类。即使你可以接受额外的依赖性，那还有另外一个问题：有时你只知道对象所实现的接口，而不知道其所属的具体类，比如可向方法的某个参数传入实现了某个接口的任何对象。

##### 解决方案

原型模式将克隆过程委派给被克隆的实际对象。模式为所有支持克隆的对象声明了一个通用接口，该接口让你能够克隆对象，同时又无需将代码和对象所属类耦合。通常情况下，这样的接口中仅包含一个**克隆方法**。

所有的类对继承的通用接口的克隆方法实现都非常相似。都是创建一个当前类的对象，然后返回一个类——即 return new Class(this);通常在构造函数中先写好初始化的样式。

其实在c#语言中已经有提供的**ICloneable接口**进行复制,就是立即可用的原型模式，但是我们可以仍然去看看并且理解这个模式是如何运行的。

##### 原型结构模式

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220809232541.png)

1.**原型(Pro­to­type)** 接口将对克隆方法进行声明。在绝大多数情况下，其中只会有一个名为 clone克隆的方法。

2.**具体原型(Con­crete Pro­to­type)** 类将实现克隆方法。除了将原始对象的数据复制到克隆体中之外，该方法有时还需处理克隆过程中的极端情况，例如克隆关联对象和梳理递归依赖等等。

3.**客户端(Client)** 可以复制实现了原型接口的任何对象。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220809233359.png)

1.**原型注册表(Pro­to­type Reg­istry)** 提供了一种访问常用原型的简单方法，其中存储了一系列可供随时复制的预生成对象。最简单的注册表原型是一个名称 → 原型的哈希表。但如果需要使用名称以外的条件进行搜索，你可以创建更加完善的注册表版本。

##### 伪代码

我会在这里附上一份伪代码以及c#官方提供的代码顺便学习这个接口。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220809233553.png)

**一份伪代码** : 通过阅读可以快速了解是如何clone的

```csharp
// 基础原型。
abstract class Shape is
    field X: int
    field Y: int
    field color: string

    // 常规构造函数。
    constructor Shape() is
        // ...

    // 原型构造函数。使用已有对象的数值来初始化一个新对象。
    constructor Shape(source: Shape) is
        this()
        this.X = source.X
        this.Y = source.Y
        this.color = source.color

    // clone（克隆）操作会返回一个形状子类。
    abstract method clone():Shape


// 具体原型。克隆方法会创建一个新对象并将其传递给构造函数。直到构造函数运
// 行完成前，它都拥有指向新克隆对象的引用。因此，任何人都无法访问未完全生
// 成的克隆对象。这可以保持克隆结果的一致。
class Rectangle extends Shape is
    field width: int
    field height: int

    constructor Rectangle(source: Rectangle) is
        // 需要调用父构造函数来复制父类中定义的私有成员变量。
        super(source)
        this.width = source.width
        this.height = source.height

    method clone():Shape is
        return new Rectangle(this)


class Circle extends Shape is
    field radius: int

    constructor Circle(source: Circle) is
        super(source)
        this.radius = source.radius

    method clone():Shape is
        return new Circle(this)


// 客户端代码中的某个位置。
class Application is
    field shapes: array of Shape

    constructor Application() is
        Circle circle = new Circle()
        circle.X = 10
        circle.Y = 10
        circle.radius = 20
        shapes.add(circle)

        Circle anotherCircle = circle.clone()
        shapes.add(anotherCircle)
        // 变量 `anotherCircle（另一个圆）`与 `circle（圆）`对象的内
        // 容完全一样。

        Rectangle rectangle = new Rectangle()
        rectangle.width = 10
        rectangle.height = 20
        shapes.add(rectangle)

    method businessLogic() is
        // 原型是很强大的东西，因为它能在不知晓对象类型的情况下生成一个与
        // 其完全相同的复制品。
        Array shapesCopy = new Array of Shapes.

        // 例如，我们不知晓形状数组中元素的具体类型，只知道它们都是形状。
        // 但在多态机制的帮助下，当我们在某个形状上调用 `clone（克隆）`
        // 方法时，程序会检查其所属的类并调用其中所定义的克隆方法。这样，
        // 我们将获得一个正确的复制品，而不是一组简单的形状对象。
        foreach (s in shapes) do
            shapesCopy.add(s.clone())

        // `shapesCopy（形状副本）`数组中包含 `shape（形状）`数组所有
        // 子元素的复制品。
```

**c#提供的ICloneable接口的代码** : 通过这里我们可以看见不需要写构造函数，只需要用到**MemberwiseClone**这个函数就可以很快地完成

```csharp
using System;

namespace RefactoringGuru.DesignPatterns.Prototype.Conceptual
{
    public class Person
    {
        public int Age;
        public DateTime BirthDate;
        public string Name;
        public IdInfo IdInfo;

        //浅复制，只复制指向某个对象的指针，而不复制对象本身，新旧对象还是共享一块内存
        //也就是说不管是修改原对象还是新对象两个都会一起改变
        public Person ShallowCopy()
        {
            return (Person)this.MemberwiseClone();
        }

        //深复制，会创造一个新的对象，但不与于原对象共享内存
        //修改新旧对象互不影响
        //所以我们可以认识到原型模式是深复制
        public Person DeepCopy()
        {
            Person clone = (Person)this.MemberwiseClone();
            clone.IdInfo = new IdInfo(IdInfo.IdNumber);
            clone.Name = String.Copy(Name);
            return clone;
        }
    }

    public class IdInfo
    {
        public int IdNumber;

        public IdInfo(int idNumber)
        {
            this.IdNumber = idNumber;
        }
    }

    //测试例子，通过例子我们可以快速的理解深复制与浅复制之间的区别
    class Program
    {
        static void Main(string[] args)
        {
            Person p1 = new Person();
            p1.Age = 42;
            p1.BirthDate = Convert.ToDateTime("1977-01-01");
            p1.Name = "Jack Daniels";
            p1.IdInfo = new IdInfo(666);

            // Perform a shallow copy of p1 and assign it to p2.
            Person p2 = p1.ShallowCopy();
            // Make a deep copy of p1 and assign it to p3.
            Person p3 = p1.DeepCopy();

            // Display values of p1, p2 and p3.
            Console.WriteLine("Original values of p1, p2, p3:");
            Console.WriteLine("   p1 instance values: ");
            DisplayValues(p1);
            Console.WriteLine("   p2 instance values:");
            DisplayValues(p2);
            Console.WriteLine("   p3 instance values:");
            DisplayValues(p3);

            // Change the value of p1 properties and display the values of p1,
            // p2 and p3.
            p1.Age = 32;
            p1.BirthDate = Convert.ToDateTime("1900-01-01");
            p1.Name = "Frank";
            p1.IdInfo.IdNumber = 7878;
            Console.WriteLine("\nValues of p1, p2 and p3 after changes to p1:");
            Console.WriteLine("   p1 instance values: ");
            DisplayValues(p1);
            Console.WriteLine("   p2 instance values (reference values have changed):");
            DisplayValues(p2);
            Console.WriteLine("   p3 instance values (everything was kept the same):");
            DisplayValues(p3);
        }

        public static void DisplayValues(Person p)
        {
            Console.WriteLine("      Name: {0:s}, Age: {1:d}, BirthDate: {2:MM/dd/yy}",
                p.Name, p.Age, p.BirthDate);
            Console.WriteLine("      ID#: {0:d}", p.IdInfo.IdNumber);
        }
    }
}
// The example displays the following output:
//       Original values of p1 and p2:
//          p1 instance values:
//             Name: Sam, Age: 42
//             Value: 6565
//          p2 instance values:
//             Name: Sam, Age: 42
//             Value: 6565
//
//       Values of p1 and p2 after changes to p1:
//          p1 instance values:
//             Name: Frank, Age: 32
//             Value: 7878
//          p2 instance values:
//             Name: Sam, Age: 42
//             Value: 7878
//
//       Values of p1 and p3 after changes to p1:
//          p1 instance values:
//             Name: George, Age: 39
//             Value: 8641
//          p3 instance values:
//             Name: Frank, Age: 32
//             Value: 7878
```

##### 适合原型模式的地方

- 如果你需要复制一些对象，同时又希望代码独立于这些对象所属的具体类，可以使用原型模式。

- 如果子类的区别仅在于其对象的初始化方式，那么你可以使用该模式来减少子类的数量。别人创建这些子类的目的可能是为了创建特定类型的对象。

##### 原型模式的优缺点

**优点** ：

- 你可以克隆对象，而无需与它们所属的具体类相耦合。
- 你可以克隆预生成原型，避免反复运行初始化代码。
- 你可以更方便地生成复杂对象。
- 你可以用继承以外的方式来处理复杂对象的不同配置。

**缺点** ：

- 克隆包含循环引用的复杂对象可能会非常麻烦。

#### Singleton(单例模式)

单例模式是一种创建型设计模式，让你能够保证一个类只有一个实例，并提供一个访问该实例的全局节点。

##### 问题

单例模式是一个十分常用的设计模式，在Unity中，它常常被用在是**Manager**类中，比如**SceneManager**,**UIManager**,**AudioManager**等等。也就是说在代码中会有一种全局类，各个模块都可以调用它。虽然它违反了单一职责原则，但由于使用起来十分方便，但还是很香的（跟全局变量一样）。

总结下来，单例模式的特点：

- 保证一个类只有一个实例
- 为该实例提供一个全局访问节点

##### 解决方案

所有单例的实现都包含以下两个相同的步骤：

- 将默认构造函数设为**私有**，防止其他对象使用单例类的new运算符。
- 新建一个静态构建方法作为构造函数。该函数会 “偷偷” 调用私有构造函数来创建对象，并将其保存在一个静态成员变量中。此后所有对于该函数的调用都将返回这一缓存对象。
如果你的代码能够访问单例类，那它就能调用单例类的静态方法。无论何时调用该方法，它总是会返回相同的对象。

##### 单例模式结构

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220810001041.png)

1.**单例(Sin­gle­ton)** 类声明了一个名为 get­Instance获取实例的静态方法来返回其所属类的一个相同实例。

单例的构造函数必须对**客户端(Client)** 代码隐藏。调用获取实例方法必须是获取单例对象的唯一方式。

##### 伪代码

由于单例模式实现过于简单，我们这里不讲伪代码，反而我们来直接看看各种的单例模式。

**懒汉单例模式** ：在第一次调用的时候实例化本身，在并发环境下，可能出现多个本身对象。所以线程是不安全的

```csharp
public class Singleton
{
    //将构造函数设置为私有，防止用户创造实例
    private Singleton() {}

    private static Singleton instance = null;

    public static Singleton GetInstance()
    {
        if(instance == null)
        {
            instance = new Singleton();
        }
        
        return instance;
    }
}
```

**简单的线程安全的懒汉单例模式** :
需要注意的是，这里使用了一个**private static object**变量进行锁定，这是因为当如果对一个外部类可以访问的对象进行锁定时会导致性能低下甚至死锁

```csharp
public class Singleton
{
    //将构造函数设置为私有，防止用户创造实例
    private Singleton{}

    private static Singleton instance = null;
    private static readonly object obj = new object ();

    public static Singleton GetInstance()
    {
        lock(obj)
        {
            if(instance == null)
            {
                instance = new Singleton();
            }
            
            return instance;
        }
    }
}
```

**双重检查锁定的懒汉单例模式** :要比前者方法更加完美

```csharp
public class Singleton
{
    //将构造函数设置为私有，防止用户创造实例
    private Singleton{}

    private static Singleton instance = null;
    private static readonly object obj = new object ();

    public static Singleton GetInstance()
    {   
        if(instace == null)
        {
            lock(obj)
            {
                if(instance == null)
                {
                    instance = new Singleton();
                }
            }    
        }
        return instance;
    }
}
```

**饿汉单例模式** :在类初始化时，已经自行实例化一个静态对象，所以本身就是线程安全的

```csharp
public class Singleton
{
    private Singleton() {}

    private static readonly Singleton instance = new Singleton();

    public static Singleton GetInstance()
    {
        return instance;
    }
}
```

饿汉单例模式实现十分简单，同时也是线程安全的，要相比懒汉单例模式更加好用一些。

##### 适合单例模式的地方

-  如果程序中的某个类对于所有客户端只有一个可用的实例，可以使用单例模式。
-  如果你需要更加严格地控制全局变量，可以使用单例模式。

##### 单例模式的优缺点

**优点** ：

- 你可以保证一个类只有一个实例。
- 你获得了一个指向该实例的全局访问节点。
- 仅在首次请求单例对象时对其进行初始化。

**缺点** ：

- 违反了单一职责原则。该模式同时解决了两个问题。
- 单例模式可能掩盖不良设计，比如程序各组件之间相互了解过多等。
- 该模式在多线程环境下需要进行特殊处理，避免多个线程多次创建单例对象。
- 单例的客户端代码单元测试可能会比较困难，因为许多测试框架以基于继承的方式创建模拟对象。由于单例类的构造函数是私有的，而且绝大部分语言无法重写静态方法，所以你需要想出仔细考虑模拟单例的方法。要么干脆不编写测试代码，或者不使用单例模式。
- 类似全局变量，在阅读代码时会产生一定困难，不知道哪里而来。

### 结构型模式(Structural Patterns)

#### Adapter(适配器模式)

适配器模式是一种结构型设计模式，它能使接口不兼容的对象能够相互合作。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220816154433.png)

上图是一个十分直观的图

##### 问题

假如你正在开发一款股票市场监测程序，它会从不同来源下载 XML 格式的股票数据，然后向用户呈现出美观的图表。在开发过程中，你决定在程序中整合一个第三方智能分析函数库。但是遇到了一个问题，那就是分析函数库只兼容 JSON 格式的数据。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220816154342.png)

##### 解决方案

你可以创建一个**适配器**。这是一个特殊的对象，能够转换对象接口，使其能与其他对象进行交互。

适配器模式通过封装对象将复杂的转换过程隐藏于幕后。被封装的对象甚至察觉不到适配器的存在。例如，你可以使用一个将所有数据转换为英制单位（如英尺和英里）的适配器封装运行于米和千米单位制中的对象。

适配器不仅可以转换不同格式的数据，其还有助于采用不同接口的对象之间的合作。它的运作方式如下：

- 适配器实现与其中一个现有对象兼容的接口。
- 现有对象可以使用该接口安全地调用适配器方法。
- 适配器方法被调用后将以另一个对象兼容的格式和顺序将请求传递给该对象。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220816154725.png)

##### 适配器模式结构

**对象适配器** ：适配器实现了其中一个对象的接口，并对另一个对象进行封装。所有流行的编程语言都可以实现适配器。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220816154822.png)

1.**客户端(Client)** 是包含当前程序业务逻辑的类。
2.**客户端接口(Client Inter­face)** 描述了其他类与客户端代码合作时必须遵循的协议。

3.**服务(Ser­vice)** 中有一些功能类 （通常来自第三方或遗留系统）。客户端与其接口不兼容，因此无法直接调用其功能。

4.**适配器(Adapter)** 是一个可以同时与客户端和服务交互的类：它在实现客户端接口的同时封装了服务对象。适配器接受客户端通过适配器接口发起的调用，并将其转换为适用于被封装服务对象的调用。

5.客户端代码只需通过接口与适配器交互即可，无需与具体的适配器类耦合。因此，你可以向程序中添加新类型的适配器而无需修改已有代码。这在服务类的接口被更改或替换时很有用：你无需修改客户端代码就可以创建新的适配器类。

**类适配器** ：这一实现使用了继承机制：适配器同时继承两个对象的接口。请注意，这种方式仅能在支持多重继承的编程语言中实现，例如C++。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220816155303.png)

1.**类适配器**不需要封装任何对象，因为它同时继承了客户端和服务的行为。适配功能在重写的方法中完成。最后生成的适配器可替代已有的客户端类进行使用。

##### 伪代码

仅仅看结构也是很难理解是啥意思的，来看看经典的方钉圆孔问题，如何将方钉用适配器转化成圆钉来适配圆孔。一样照着之前，写一个不是那么伪的伪代码

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220816155544.png)

```csharp
//圆孔类(RoundHole)和圆钉类(RoundPeg)互相兼容 
public class RoundHole 
{
    private int radius;

    public RoundHole(int radius)
    {
        //...
    }
    public int getRadius()
    {
        //
    }
    public bool fits(RoundPeg peg)
    {
        return this.getRadius() >= peg.getRadius();
    }
}
public class RoundPeg
{
    private int radius;

    public RoundPeg(int radius)
    {
        //...
    }

    public int getRadius()
    {
        //...
    }
}
//不兼容的方钉(SquarePeg)类
public class SquarePeg
{
    private int width;

    public SquarePeg(int width)
    {
        //...
    }

    public int getWidth()
    {
        //...
    }
}
//适配器类其实就是圆钉的子类，算是特殊的圆钉类，将获得的方钉“打磨”成圆钉
public class SquarePegAdapter : RoundPeg
{
    //适配器通常包含一个要被转换的实例
    private SquarePeg peg;

    public SquarePegAdapter(SquarePeg peg)
    {
        this.peg = peg;
    }

    public int getRadius()
    {
        return peg.getWidth() * Math.sqrt(2) / 2;
    }
}
//客户端代码
hole = new RoundHole(5);

_sqpeg = new SquarePeg(5);

sqpeg_adapter = new SquarePegAdapter(_sqpeg);
hole.fits(sqpeg_adapter);
//变换之后，我们进行操作的就是适配器类而不是方钉类了
```

##### 适合适配器模式的地方

- 当你希望使用某个类，但是其接口与其他代码不兼容时，可以使用适配器类。也就是创造一个中间层类，如果你在前人的代码修改但是又不打算修改太多
- 如果您需要复用这样一些类，他们处于同一个继承体系，并且他们又有了额外的一些共同的方法，但是这些共同的方法不是所有在这一继承体系中的子类所具有的共性。

##### 适配器模式的优缺点

**优点** ：

- 符合SRP
- 符合OCP

**缺点** ：

- 代码整体复杂度增加，因为你需要新增一系列接口和类。有时直接更改服务类使其与其他代码兼容会更简单。

#### Bridge(桥接模式)

桥接模式是一种结构型设计模式，可将一个大类或一系列紧密相关的类拆分为抽象和实现两个独立的层次结构，从而能在开发时分别使用。

##### 问题

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220816163009.png)

假如你有一个几何形状**Shape**类，从它能扩展出两个子类：​圆形**Cir­cle**和方形**Square**。你希望对这样的类层次结构进行扩展以使其包含颜色，所以你打算创建名为红色**Red**和 蓝色**Blue**的形状子类。但是，由于你已有两个子类，所以总共需要创建四个类才能覆盖所有组合，例如蓝色圆形**Blue­Cir­cle**和红色方形**Red­Square**。在层次结构中新增形状和颜色将导致代码复杂程度指数增长。例如添加三角形状，你需要新增两个子类，也就是每种颜色一个；此后新增一种新颜色需要新增三个子类，即每种形状一个。如此以往，情况会越来越糟糕。

##### 解决方案

问题的根本原因是我们试图在两个独立的维度——形状与颜色——上扩展形状类。这在处理类继承时是很常见的问题。

桥接模式通过将继承改为组合的方式来解决这个问题。具体来说，就是抽取其中一个维度并使之成为独立的类层次，这样就可以在初始类中引用这个新层次的对象，从而使得一个类不必拥有所有的状态和行为。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220816163706.png)

根据该方法，我们可以将颜色相关的代码抽取到拥有 红色和 蓝色两个子类的颜色类中，然后在形状类中添加一个指向某一颜色对象的引用成员变量。现在，形状类可以将所有与颜色相关的工作委派给连入的颜色对象。这样的引用就成为了 形状和 颜色之间的桥梁。此后，新增颜色将不再需要修改形状的类层次，反之亦然。

##### 桥接模式结构

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220816164716.png)

1.**抽象部分(Abstrac­tion)** 提供高层控制逻辑， 依赖于完成底层实际工作的实现对象。

2.**实现部分(Imple­men­ta­tion)** 为所有具体实现声明通用接口。抽象部分仅能通过在这里声明的方法与实现对象交互。抽象部分可以列出和实现部分一样的方法，但是抽象部分通常声明一些复杂行为，这些行为依赖于多种由实现部分声明的原语操作。

3.**具体实现(Con­crete Imple­men­ta­tions)** 中包括特定于平台的代码。

4.**精确抽象(Refined Abstrac­tion)**提供控制逻辑的变体。与其父类一样，它们通过通用实现接口与不同的实现进行交互。

5.通常情况下，**客户端(Client)**仅关心如何与抽象部分合作。但是，客户端需要将抽象对象与一个实现对象连接起来。

##### 伪代码

在这次不那么伪的伪代码中我打算展现两段，其中一个是之前的Shape和Color之间的桥接。首先我们来看看遥控器遥控设备，是很容易理解设备就是实现部分，而遥控为抽象设备。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220816170510.png)

遥控器基类声明了一个指向设备对象的引用成员变量。 所有遥控器通过通用设备接口与设备进行交互，使得同一个遥控器可以支持不同类型的设备。
你可以开发独立于设备类的遥控器类，只需新建一个遥控器子类即可。例如，基础遥控器可能只有两个按钮，但你可在其基础上扩展新功能，比如额外的一节电池或一块触摸屏。

```csharp
// “抽象部分”定义了两个类层次结构中“控制”部分的接口。它管理着一个指向“实
// 现部分”层次结构中对象的引用，并会将所有真实工作委派给该对象。
public class Remote
{
    private Device device;
    
    public Remote(Device device) 
    {
        this.device = device;
    }

    public void togglePower()
    {
        if(device.isEnabled())
        {
            device.disable();
        }
        else 
        {
            //..
        }
    }

    public void volumeUp()
    {
        device.setVolume(device.getVolume() + 10);
    }

    public void volumeDown()
    {
        //..
    }

    public void ChannelUp()
    {
        device.setChannel(device.getChannel() + 1)
    }

    public void ChannelDown()
    {
        //..
    }
}
// 你可以独立于设备类的方式从抽象层中扩展类。
public class AdvancedRemote : Remote
{
    public void mute()
    {
        device.setVolume(0);
    }
}
// “实现部分”接口声明了在所有具体实现类中通用的方法。它不需要与抽象接口相
// 匹配。实际上，这两个接口可以完全不一样。通常实现接口只提供原语操作，而
// 抽象接口则会基于这些操作定义较高层次的操作。
public interface Device 
{
    bool isEnable();
    void enable();
    void disable();
    int getVolume();
    void setVolume(..);
    int getChannel();
    void setChannel(..);
}
public class TV : Device 
{
    //...
}
public vlass Radio : Device
{
    //..
}

// 客户端代码
tv = new Tv();
remote = new RemoteControl(tv);
remote.togglePower();

radio = new Radio();
remote = new AdvancedRemoteControl(radio);
```

对于Shape和Color我们可能很难区别谁是“抽象”，谁是“实现”，但是桥接模式同样适合拆分类的结构,即抽取复杂类的其中一个维度使之成为独立的类层次。

```csharp
public class Shape
{
    private Color color;

    //..
}
public class Circle : Shape
{
    //..
}

public class Square : Shape
{
    //..
}

public interface Color 
{
    //..
}

public class Red : Color 
{
    //..
}
public class Blue : Color
{
    //..
}
```

##### 适合桥接模式的地方

- 如果你想要拆分或重组一个具有多重功能的庞杂类 （例如能与多个数据库服务器进行交互的类），可以使用桥接模式。桥接模式可以将庞杂类拆分为几个类层次结构。此后，你可以修改任意一个类层次结构而不会影响到其他类层次结构。这种方法可以简化代码的维护工作，并将修改已有代码的风险降到最低。
- 如果你希望在几个独立维度上扩展一个类，可使用该模式。
- 如果你需要在运行时切换不同实现方法，可使用桥接模式。

##### 桥接模式的优缺点

**优点** ：

- 你可以创建与平台无关的类和程序。
- 客户端代码仅与高层抽象部分进行互动，不会接触到平台的详细信息。
- 符合OCP
- 符合SRP

**缺点** ：

- 对高内聚的类使用该模式可能会让代码更加复杂。

#### Composite(组合模式)

组合模式是一种结构型设计模式，你可以使用它将对象组合成树状结构，并且能像使用独立对象一样使用它们。

##### 问题

**如果应用的核心模型能用树状结构表示，在应用中使用组合模式才有价值。**例如，你有两类对象： ​ 产品和盒子。一个盒子中可以包含多个产品或者几个较小的盒子。这些小盒子中同样可以包含一些产品或更小的盒子，以此类推。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220818150134.png)

订单中可能包括各种产品，这些产品放置在盒子中，然后又被放入一层又一层更大的盒子中。整个结构看上去像是一棵倒过来的树。你可以尝试直接计算：打开所有盒子，找到每件产品，然后计算总价。这在真实世界中或许可行，但在程序中，你并不能简单地使用循环语句来完成该工作。你必须事先知道所有产品和盒子的类别，所有盒子的嵌套层数以及其他繁杂的细节信息。因此，直接计算极不方便，甚至完全不可行。

##### 解决方案

组合模式建议使用一个通用接口来与产品和盒子进行交互，并且在该接口中声明一个计算总价的方法。那么方法该如何设计呢？对于一个产品，该方法直接返回其价格；对于一个盒子，该方法遍历盒子中的所有项目，询问每个项目的价格，然后返回该盒子的总价格。如果其中某个项目是小一号的盒子，那么当前盒子也会遍历其中的所有项目，以此类推，直到计算出所有内部组成部分的价格。你甚至可以在盒子的最终价格中增加额外费用，作为该盒子的包装费用。**类似于树的递归遍历**
该方式的最大优点在于你无需了解构成树状结构的对象的具体类。你也无需了解对象是简单的产品还是复杂的盒子。你只需调用通用接口以相同的方式对其进行处理即可。当你调用该方法后，对象会将请求沿着树结构传递下去。

##### 组合模式结构

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220818150405.png)

1.**组件(Com­po­nent)** 接口描述了树中简单项目和复杂项目所共有的操作。

2.**叶节点(Leaf)** 是树的基本结构，它不包含子项目。
一般情况下，叶节点最终会完成大部分的实际工作， 因为它们无法将工作指派给其他部分。

3.**容器(Con­tain­er)** ——又名 **“组合 (Com­pos­ite)”**——是包含叶节点或其他容器等子项目的单位。容器不知道其子项目所属的具体类，它只通过通用的组件接口与其子项目交互。
容器接收到请求后会将工作分配给自己的子项目，处理中间结果，然后将最终结果返回给客户端。

4.**客户端(Client)** 通过组件接口与所有项目交互。因此，客户端能以相同方式与树状结构中的简单或复杂项目交互。

##### 伪代码

一个例子是利用组合模式在图形编辑器中实现一系列的几何图形。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220818151017.png)

```csharp
public interface Graphic 
{
    void move(x,y);

    void draw();
}
//Dot类是叶节点，不能能包含任何子对象，通常完成所有工作
public class Dot : Graphic 
{
    private T x,y;

    public Dot(T x,T y)
    {
        //..
    }

    public void move(T x,T y)
    {
        this.x += x,this.y +=y;
    }

    public void draw()
    {
        //..
    }
}
//所有的组件类都可以拓展
public class Circle : Dot
{
    private T radius;

    public Circle(T x,T y,T radius)
    {
        //..
    }

    void draw()
    {
        //...
    }
}
//CompoundGraphic类是复杂组件，也就是树中的非叶子节点
public class CompoundGraphic : Graphic
{
    private Graphic[] chidren;

    public void add(Graphic child)
    {
        //添加至chidren数组
    }

    public void remove(Graphic child)
    {
        //移除chidren数组里的一个child
    }

    //遍历每一个child，让child来做具体的事情
    public void move(x,y)
    {
        foreach (var child in children)
        {
            child.move(x,y);
        }
    }

    public void draw()
    {
        //分两步，一个是画完所有child的内容
        //第二步是根据自身内容画点东西
    }
}

//简明的客户端代码

CompoundGraphic tree = new CompoundGraphic();
CompoundGraphic branch1 = new CompoundGraphic();
branch1.Add(new Dot(1,2));
branch1.Add(new Dot(3,4));
CompoundGraphic branch2 = new CompoundGraphic();
branch2.Add(new Circle(5,6,3));
branch2.Add(new Dot(7,8));
branch3.Add(new Dot(9,10));
tree.Add(branch1);
tree.Add(branch2);

tree.move(1,2);
tree.draw();
```

##### 适合组合模式的地方

- 如果你需要实现**树状对象结构**，可以使用组合模式。
- 如果你希望客户端代码以**相同方式处理简单和复杂元素**，可以使用该模式。

##### 组合模式的优缺点

**优点** ：

- 你可以利用**多态**和**递归**机制更方便地使用复杂树结构。
- 符合OCP

**缺点** ：

- 对于功能差异较大的类，提供公共接口或许会有困难。在特定情况下，你需要过度一般化组件接口，使其变得令人难以理解。

#### Decorator(装饰模式)

装饰模式是一种结构型设计模式，允许你通过将对象放入包含行为的特殊封装对象中来为原对象绑定新的行为。

##### 问题

假设你正在开发一个提供通知功能的库，其他程序可使用它向用户发送关于重要事件的通知。
库的最初版本基于**通知器Noti­fi­er类**，其中只有很少的几个成员变量，一个构造函数和一个send发送方法。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220818203702.png)

此后某个时刻，你会发现库的用户希望使用除邮件通知之外的功能。许多用户会希望接收关于紧急事件的手机短信，还有些用户希望在微信上接收消息，而公司用户则希望在 QQ 上接收消息。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220818203808.png)

首先扩展通知器类，然后在新的子类中加入额外的通知方法。现在客户端要对所需通知形式的对应类进行初始化，然后使用该类发送后续所有的通知消息。但是很快有人会问：​“为什么不同时使用多种通知形式呢？如果房子着火了，你大概会想在所有渠道中都收到相同的消息吧。”你可以尝试创建一个特殊子类来将多种通知方法组合在一起以解决该问题。但这种方式会使得代码量迅速膨胀，不仅仅是程序库代码，客户端代码也会如此。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220818203913.png)

##### 解决方案

当你需要更改一个对象的行为时，第一个跳入脑海的想法就是扩展它所属的类。但是，你不能忽视继承可能引发的几个严重问题。

- 继承是静态的。你无法在运行时更改已有对象的行为，只能使用由不同子类创建的对象来替代当前的整个对象。
- 子类只能有一个父类。大部分编程语言不允许一个类同时继承多个类的行为。

其中一种方法是用**聚合或组合(has a/contains a)** ，而不是继承。两者的工作方式几乎一模一样：一个对象包含指向另一个对象的引用，并将部分工作委派给引用对象；继承中的对象则继承了父类的行为，它们自己能够完成这些工作。你可以使用这个新方法来轻松替换各种连接的 “小帮手” 对象，从而能在运行时改变容器的行为。一个对象可以使用多个类的行为， 包含多个指向其他对象的引用，并将各种工作委派给引用对象**聚合（或组合） 组合是许多设计模式背后的关键原则 （包括装饰在内）。记住这一点后，让我们继续关于模式的讨论**。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220818204142.png)

那么什么时候一个简单的封装器可以被称为是真正的装饰呢？正如之前提到的，封装器实现了与其封装对象相同的接口。因此从客户端的角度来看，这些对象是**完全一样**的。封装器中的引用成员变量可以是遵循相同接口的任意对象。这使得你可以将**一个对象放入多个封装器**中，并在对象中添加所有这些封装器的组合行为。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220818205047.png)

##### 装饰模式结构

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220818205848.png)

1.**部件(Com­po­nent)** 声明封装器和被封装对象的公用接口。

2.**具体部件(Con­crete Com­po­nent)** 类是被封装对象所属的类。 它定义了基础行为， 但装饰类可以改变这些行为。

3.**基础装饰(Base Dec­o­ra­tor)** 类拥有一个指向被封装对象的引用成员变量。 该变量的类型应当被声明为通用部件接口， 这样它就可以引用具体的部件和装饰。 装饰基类会将所有操作委派给被封装的对象。

4.**具体装饰类(Con­crete Dec­o­ra­tors)** 定义了可动态添加到部件的额外行为。 具体装饰类会重写装饰基类的方法， 并在调用父类方法之前或之后进行额外的行为。

5.**客户端(Client)** 可以使用多层装饰来封装部件， 只要它能使用通用接口与所有对象互动即可。

##### 伪代码

仅仅看上面的内容只是知道个大概，来看看更具体的例子以及写写一些不那么伪的伪代码。

**第一个例子，c#类型的大概结构** :

```csharp
//定义抽象Component类，准备被具体Component类和Base Decorator类继承
public abstract class Component
{
    public abstract string Operation();
}
//具体Component类定义了基础行为，装饰器就是修饰这些行为
//比如说你要画一个圆，这是本身要干的事情
//如果要画一个红色的圆，可以用修饰器来修饰这个行为
public class ConcreteComponent : Component
{
    public override string Operation()
    {
        return "ConcreteComponent";
    }
}
//装饰器要跟具体组件继承相同的类
//该类主要为了定义所有具体装饰类的接口。
//通常有一个关于Component的成员变量,并且要初始化
public abstract class Decorator : Component
{
    protected Component _component;

    //初始化
    public Decorator(Component component)
    {
        this._component = component;
    }

    public override string Operation()
    {
        if (this._component != null)
        {
            return this._component.Operation();
        }
        else
        {
            return string.Empty;
        }
    }
}
public class ConcreteDecoratorA : Decorator
{
    public ConcreteDecoratorA(Component component) : base(component)
    {
        //继承初始化
    }

    public override string Operation()
    {
        return $"ConcreteDecoratorA({base.Operation()})";
    }   
}
public class ConcreteDecoratorB : Decorator
{
    public ConcreteDecoratorB(Component component) : base(component)
    {
        //继承初始化
    }

    public override string Operation()
    {
        return $"ConcreteDecoratorB({base.Operation()})";
    }   
}
public class Client
{
    public void ClientCode(Component component)
    {
        Console.WriteLine("RESULT: " + component.Operation());
    }
}

//客户端代码
Client client = new Client();

var simple = new ConcreteComponent();
 Console.WriteLine("Client: I get a simple component:");
client.ClientCode(simple);
Console.WriteLine();

ConcreteDecoratorA decorator1 = new ConcreteDecoratorA(simple);
ConcreteDecoratorB decorator2 = new ConcreteDecoratorB(decorator1);
Console.WriteLine("Client: Now I've got a decorated component:");
client.ClientCode(decorator2);

/*演示结果
Client: I get a simple component:
RESULT: ConcreteComponent

Client: Now I've got a decorated component:
RESULT: ConcreteDecoratorB(ConcreteDecoratorA(ConcreteComponent))
*/
```

上一个例子基本上可以知道大概的运作方式，但是对于使用还不能够了解，接下来看一个比较简单的例子，可以很容易体现装饰器是在**装饰具体组件的行为**，感觉就跟c#一样，如果**Component**相当于c#的抽象类，那么**Decorator**就相当于c#的接口（但是实际上c#的接口不能继承类）

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220818212043.png)

图是java的示意图，但是我这里用c#写出来

```csharp
//Component类
public abstract class Shape
{
    public abstract void draw();
}
//Concrete Component 类
public class Rectangle : Shape
{
    public override void draw()
    {
        Console.WriteLine("Shape:Rectangle");
    }
}
//Concrete Component 类
public class Circle : Shape
{
    public override void draw()
    {
        Console.WriteLine("Shape:Circle");
    }
}
//抽象Base Decorator类
public abstract class ShapeDecorator : Shape
{
    protected Shape decoratedShape;

    public ShapeDecorator(Shape shape)
    {
        this.decoratedShape = shape;
    }

    public override void draw()
    {
        decoratedShape.draw();
    }
}
//Concrete Decorator类
public class RedShapeDecorator : ShapeDecorator
{
    public RedShapeDecorator(Shape shape) : base (shape)
    {
        //继承初始化
    }

    public override void draw()
    {
        Console.Write("Red + ");
        base.draw();
    }
}
//客户端代码
var circle = new Circle();
ShapeDecorator redCircle = new RedShapeDecorator(new Circle());
ShapeDecorator redRectangle = new RedShapeDecorator(new Rectangle());

Console.WriteLine("Circle with normal border");
circle.draw();

Console.WriteLine("\nCircle of red border");
redCircle.draw();

Console.WriteLine("\nRectangle of red border");
redRectangle.draw();

/*运行结果
Circle with normal border
Shape:Circle

Circle of red border
Red + Shape:Circle

Rectangle of red border
Red + Shape:Rectangle
*/
```

##### 适合装饰模式的地方

- 如果你希望在无需修改代码的情况下即可使用对象，且希望在运行时为对象新增额外的行为，可以使用装饰模式。
- 如果用继承来扩展对象行为的方案难以实现或者根本不可行，你可以使用该模式。

##### 装饰模式的优缺点

**优点** ：

- 你无需创建新子类即可扩展对象的行为。
- 你可以在运行时添加或删除对象的功能。
- 你可以用多个装饰封装对象来组合几种行为。
- 符合SRP

**缺点** ：

- 在封装器栈中删除特定封装器比较困难。
- 实现行为不受装饰栈顺序影响的装饰比较困难。
- 各层的初始化配置代码看上去可能会很糟糕。

#### Fecade(外观模式/门面模式)

外观模式是一种结构型设计模式，能为程序库、框架或其他复杂类提供一个简单的接口。

##### 问题

假设你必须在代码中使用某个**复杂的库或框架中的众多对象**。正常情况下，你需要负责所有对象的初始化工作、管理其依赖关系并按正确的顺序执行方法等。最终，程序中类的业务逻辑将与第三方类的实现细节紧密耦合，使得理解和维护代码的工作很难进行。

##### 解决方案

外观类为包含许多活动部件的**复杂子系统提供一个简单的接口**。与直接调用子系统相比， 外观提供的功能可能比较有限， 但它却包含了客户端真正关心的功能。

##### 外观模式结构

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220818223832.png)

1.**外观(Facade)** 提供了一种访问特定子系统功能的便捷方式， 其了解如何重定向客户端请求， 知晓如何操作一切活动部件。

2.**创建附加外观(Addi­tion­al Facade)**类可以避免多种不相关的功能污染单一外观， 使其变成又一个复杂结构。 客户端和其他外观都可使用附加外观。

3.**复杂子系统(Com­plex Sub­sys­tem)** 由数十个不同对象构成。如果要用这些对象完成有意义的工作，你必须深入了解子系统的实现细节，比如按照正确顺序初始化对象和为其提供正确格式的数据。
子系统类不会意识到外观的存在，它们在系统内运作并且相互之间可直接进行交互。

4.**客户端(Client)** 使用外观代替对子系统对象的直接调用。

##### 伪代码

在本例中，外观模式简化了客户端与复杂视频转换框架之间的交互。你可以创建一个封装所需功能并隐藏其他代码的外观类，从而无需使全部代码直接与数十个框架类进行交互。该结构还能将未来框架升级或更换所造成的影响最小化，因为你只需修改程序中外观方法的实现即可。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220818224224.png)

```csharp
//各种子系统类
public class VideoFile
{
    // ...
}
public class OggCompressionCodec
{
    // ...
}
public class MPEG4CompressionCodec
{
    // ...
}
public class CodecFactory
{
    // ...
}
public class BitrateReader
{
    // ...
}
public class AudioMixer
{
    // ...
}

//一个外观类，目的是为了将很多的子系统类转换成一个接口来给客户端看
public class VideoConverter
{
    //假设返回类型就是File类
    //不要在意里面的具体内容，只用知道这是个转化器就行了
    public File converter(filename,format)
    {
        File file = new VideoFile(filename);
        CodecFactory sourceCodec = new CodecFactory.extract(file);
        if (format == "mp4")
            MPEG4CompressionCodec destinationCodec = new MPEG4CompressionCodec();
        else
            OggCompressionCodec destinationCodec = new OggCompressionCodec();
        BitrateReader buffer = BitrateReader.read(filename, sourceCodec);
        BitrateReader result = BitrateReader.convert(buffer, destinationCodec);
        AudioMixer result = (new AudioMixer()).fix(result);
        return new File(result);
    }
}

//客户端代码
var convertor = new VideoConverter();
var mp4 = convertor.convert("funny-cats-video.ogg", "mp4")
mp4.save()
```

##### 适合外观模式的地方

- 如果你需要一个指向复杂子系统的直接接口，且该接口的功能有限，则可以使用外观模式。
- 如果需要将子系统组织为多层结构，可以使用外观。

##### 外观模式的优缺点

**优点** ：

- 你可以让自己的代码独立于复杂子系统。

**缺点** ：

- 外观可能成为与程序中所有类都耦合的上帝对象（一个上帝对象(God object)是一个了解过多或者负责过多的对象）

#### Flyweight(享元模式)

享元模式是一种结构型设计模式，它摒弃了在每个对象中保存所有数据的方式，通过共享多个对象所共有的相同状态，让你能在有限的内存容量中载入更多对象。简单来说，就是提取一个大类中共同的不变的内容的为一个类和一个需要经常生成的变化状态的类。

##### 问题

真正的问题与粒子系统有关。每个粒子 （一颗子弹、 一枚导弹或一块弹片） 都由包含完整数据的独立对象来表示。当玩家在游戏中鏖战进入高潮后的某一时刻，游戏将无法在剩余内存中载入新建粒子，于是程序就崩溃了。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220818230038.png)

##### 解决方案

仔细观察**粒子Par­ti­cle类**， 你可能会注意到**颜色(color)和精灵图(sprite)**这两个成员变量所消耗的内存要比其他变量多得多。更糟糕的是，对于所有的粒子来说，**这两个成员变量所存储的数据几乎完全一样** （比如所有子弹的颜色和精灵图都一样）。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220818230148.png)

每个粒子的另一些状态 （坐标、 移动矢量和速度） 则是不同的。因为这些成员变量的数值会不断变化。 这些数据代表粒子在存续期间不断变化的情景，但每个粒子的颜色和精灵图则会保持不变。
对象的常量数据通常被称为**内在状态**，其位于对象中，其他对象只能读取但不能修改其数值。而对象的其他状态常常能被其他对象 “从外部” 改变，因此被称为**外在状态**。
我们将这样一个**仅存储内在状态的对象称为享元**。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220818230930.png)

**享元与不可变性** :
由于享元对象可在不同的情景中使用，你必须确保其状态不能被修改。**享元类的状态只能由构造函数的参数进行一次性初始化**，它不能对其他对象公开其设置器或公有成员变量。

**享元工厂** :
为了能更方便地访问各种享元，你可以创建一个工厂方法来管理已有享元对象的缓存池。工厂方法从客户端处接收目标享元对象的内在状态作为参数，如果它能在缓存池中找到所需享元，则将其返回给客户端；如果没有找到，它就会新建一个享元，并将其添加到缓存池中。
你可以选择在程序的不同地方放入该函数。最简单的选择就是将其放置在享元容器中。除此之外，你还可以新建一个工厂类，或者创建一个静态的工厂方法并将其放入实际的享元类中。

##### 享元模式结构

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220818231129.png)

1.享元模式只是一种优化。在应用该模式之前，你要确定程序中存在与大量类似对象同时占用内存相关的内存消耗问题，并且确保该问题无法使用其他更好的方式来解决。

2.**享元(Fly­weight)** 类包含原始对象中部分能在多个对象中共享的状态。 同一享元对象可在许多不同情景中使用。 享元中存储的状态被称为 “内在状态”。 传递给享元方法的状态被称为 “外在状态”。

3.**情景(Con­text)** 类包含原始对象中各不相同的外在状态。 情景与享元对象组合在一起就能表示原始对象的全部状态。

4.通常情况下，原始对象的行为会保留在享元类中。因此调用享元方法必须提供部分外在状态作为参数。但你也可将行为移动到情景类中，然后将连入的享元作为单纯的数据对象。

5.**客户端(Client)** 负责计算或存储享元的外在状态。在客户端看来，享元是一种可在运行时进行配置的模板对象，具体的配置方式为向其方法中传入一些情景数据参数。

6.**享元工厂(Fly­weight Fac­to­ry)** 会对已有享元的缓存池进行管理。有了工厂后，客户端就无需直接创建享元，它们只需调用工厂并向其传递目标享元的一些内在状态即可。工厂会根据参数在之前已创建的享元中进行查找，如果找到满足条件的享元就将其返回；如果没有找到就根据参数新建享元。

##### 伪代码

在本例中，享元模式能有效减少在画布上渲染数百万个树状对象时所需的内存。该模式从主要的**树Tree**类中抽取内在状态，并将其移动到**享元类树种类Tree­Type**之中。

```csharp
//享元类,拥有大量共同的名字，颜色和材质
//如果每个树都进行一次保存将会消耗大量的内存
public class TreeType
{
    private string name;
    private Color color;
    private Texture texture;

    public TreeType(name,color,texture)
    {
        //...
    }
    public draw(canvas,x,y)
    {
        // 1. 创建特定类型、颜色和纹理的位图。
        // 2. 在画布坐标 (X,Y) 处绘制位图。
    }
}

//使用享元工厂，当然是不一定只有一种树啦
public class TreeFactory
{
    public static TreeType[] treeTypes;
    public static TreeType getTreeType(name,color,texture)
    {
        TreeType type = treeTypes.Find(name,color,texture);
        if(type == null)
        {
            type = new TreeType(name,color,texture);
            treeTypes.add(type);
        }
        return type;
    }
}

//树的外在状态
public class Tree 
{
    public float x,y;
    public TreeType type;
    
    public Type(x,y,type)
    {
        //..
    }
    public void draw(canvas)
    {
        type.draw(canvas,this.x,this.y);
    }
}

// 树（Tree）和森林（For­est）类是享元的客户端。
// 如果不打算继续对树类进行开发，你可以将它们合并。
public class Forest
{
    public Tree[] trees;

    public void plantTree(x,y,name,color,texture)
    {
        TreeType type = TreeFactory.getTreeType(name,color,texture);
        tree = new Tree(x,y,type);
        trees.add(tree);
    }

    public void draw(canvas)
    {
        foreach(var tree in trees)
        {
            tree.draw(canvas);
        }
    }
}
```

##### 适合享元模式的地方

- 仅在程序必须支持**大量对象且没有足够的内存容量**时使用享元模式(比如粒子系统)。

##### 享元模式的优缺点

**优点** ：

- 如果程序中有很多相似对象，那么你将可以节省大量内存。

**缺点** ：

- 你可能需要牺牲执行速度来换取内存，因为他人每次调用享元方法时都需要重新计算部分情景数据。
- 代码会变得更加复杂。 团队中的新成员总是会问： ​“为什么要像这样拆分一个实体的状态？”。

#### Proxy(代理模式)

代理模式是一种结构型设计模式，让你能够提供对象的替代品或其占位符。代理控制着对于原对象的访问，并允许在将请求提交给对象前后进行一些处理。

##### 问题

为什么要控制对于某个对象的访问呢？ 举个例子： 有这样一个消耗大量系统资源的巨型对象，你只是偶尔需要使用它，并非总是需要。你可以实现延迟初始化：在实际有需要时再创建该对象。对象的所有客户端都要执行延迟初始代码。不幸的是，这很可能会带来很多重复代码。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220819001221.png)

在理想情况下，我们希望将代码直接放入对象的类中，但这并非总是能实现：比如类可能是第三方封闭库的一部分。

##### 解决方案

代理模式建议新建一个与原服务对象接口相同的代理类，然后更新应用以将代理对象传递给所有原始对象客户端。代理类接收到客户端请求后会创建实际的服务对象，并将所有工作委派给它。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220819001254.png)

##### 代理模式结构

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220819001317.png)

1.**服务接口(Ser­vice Inter­face)** 声明了服务接口。代理必须遵循该接口才能伪装成服务对象。

2.**服务(Ser­vice)** 类提供了一些实用的业务逻辑。

3.**代理(Proxy)** 类包含一个指向服务对象的引用成员变量。代理完成其任务（例如延迟初始化、记录日志、访问控制和缓存等）后会将请求传递给服务对象。通常情况下，代理会对其服务对象的整个生命周期进行管理。

4.**客户端(Client)** 能通过同一接口与服务或代理进行交互，所以你可在一切需要服务对象的代码中使用代理。

##### 伪代码

代理模式虽然在绝大多数c#程序中十分不常见，但是在一些特殊情况下使用还是很方便的。我们仅仅在这里对着结构图写一个仍然不是那么伪的伪代码

```csharp
//该服务接口是代理类和真实服务类必须要声明的
public interface ServiceInterface
{
    void Operation();
}
//真实的服务类
public class Service : ServiceInterface
{
    public void Operation()
    {
        Console.WriteLine("...");
    }
}
//代理类
public class Proxy : ServiceInterface
{
    private Service _service;

    public Proxy(Service service)
    {
        this._service = service;
    }

    public void Operation()
    {
        if(this.CheckAccess())
        {
            this._service.Operation();
        }
    }

    public bool CheckAccess()
    {
        //一些真实的Check代码段，但是这里就省略了
        //...

        return true;
    }
}
//客户端代码
Console.WriteLine("Client: Executing the client code with a real subject:");
var service = new Service();
service.Operation();

Console.WriteLine();

Console.WriteLine("Client: Executing the same client code with a proxy:");

Proxy proxy = new Proxy(service);
proxy.Operation();
```

##### 适合代理模式的地方

- 延迟初始化（虚拟代理）。如果你有一个偶尔使用的重量级服务对象，一直保持该对象运行会消耗系统资源时，可使用代理模式。
- 访问控制（保护代理）。如果你只希望特定客户端使用服务对象，这里的对象可以是操作系统中非常重要的部分，而客户端则是各种已启动的程序（包括恶意程序），此时可使用代理模式。
- 本地执行远程服务（远程代理）。适用于服务对象位于远程服务器上的情形。
- 记录日志请求（日志记录代理）。适用于当你需要保存对于服务对象的请求历史记录时。
- 缓存请求结果（缓存代理）。适用于需要缓存客户请求结果并对缓存生命周期进行管理时，特别是当返回结果的体积非常大时。
- 智能引用。可在没有客户端使用某个重量级对象时立即销毁该对象。

##### 代码模式的优缺点

**优点** ：

- 你可以在客户端毫无察觉的情况下控制服务对象。
- 如果客户端对服务对象的生命周期没有特殊要求，你可以对生命周期进行管理。
- 即使服务对象还未准备好或不存在，代理也可以正常工作。
- 符合OCP

**缺点** :

- 代码可能会变得复杂，因为需要新建许多类。
- 服务响应可能会延迟。

### 行为模式(Behavioral Patterns)

#### Chain of Responsibility(责任链模式)

责任链模式是一种行为设计模式，允许你将请求沿着处理者链进行发送。收到请求后，每个处理者均可对请求进行处理，或将其传递给链上的下个处理者。

##### 问题

假如你正在开发一个在线订购系统。你希望对系统访问进行限制，只允许认证用户创建订单。此外，拥有管理权限的用户也拥有所有订单的完全访问权限。简单规划后，你会意识到这些检查必须依次进行。只要接收到包含用户凭据的请求，应用程序就可尝试对进入系统的用户进行认证。但如果由于用户凭据不正确而导致认证失败，那就没有必要进行后续检查了。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220824130805.png)

在接下来的几个月里，你实现了后续的几个检查步骤。

- 一位同事认为直接将原始数据传递给订购系统存在安全隐患。因此你新增了额外的验证步骤来清理请求中的数据。
- 过了一段时间，有人注意到系统无法抵御暴力密码破解方式的攻击。为了防范这种情况你立刻添加了一个检查步骤来过滤来自同一IP地址的重复错误请求。
- 又有人提议你可以对包含同样数据的重复请求返回缓存中的结果，从而提高系统响应速度。因此，你新增了一个检查步骤，确保只有没有满足条件的缓存结果时请求才能通过并被发送给系统。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220824130901.png)

##### 解决方案

与许多其他行为设计模式一样，责任链会将特定行为转换为被称作**处理者的独立对象**。在上述示例中，每个检查步骤都可被抽取为仅有单个方法的类，并执行检查操作。请求及其数据则会被作为参数传递给该方法。
模式建议你**将这些处理者连成一条链**。链上的每个处理者都有一个成员变量来保存对于下一处理者的引用。除了处理请求外，处理者还负责沿着链传递请求。请求会在链上移动，直至所有处理者都有机会对其进行处理。最重要的是：**处理者可以决定不再沿着链传递请求，这可高效地取消所有后续处理步骤**。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220824131142.png)

不过还有一种稍微不同的方式 （也是更经典一种）， 那就是**处理者接收到请求后自行决定是否能够对其进行处理**。如果自己能够处理，处理者就不再继续传递请求。因此在这种情况下，每个请求要么最多有一个处理者对其进行处理，要么没有任何处理者对其进行处理。在处理图形用户界面元素栈中的事件时，这种方式非常常见。
所有**处理者类均实现同一接口**是关键所在。每个具体处理者仅关心下一个包含exe­cute执行方法的处理者。这样一来，你就可以在运行时使用不同的处理者来创建链，而无需将相关代码与处理者的具体类进行耦合。

##### 责任链模式结构

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220824131355.png)

1.**处理者(Han­dler)** 声明了所有具体处理者的通用接口。该接口通常仅包含单个方法用于请求处理， 但有时其还会包含一个设置链上下个处理者的方法。

2.**基础处理者(Base Han­dler)** 是一个可选的类，你可以将所有处理者共用的样本代码放置在其中。
通常情况下，该类中定义了一个保存对于下个处理者引用的成员变量。客户端可通过将处理者传递给上个处理者的构造函数或设定方法来创建链。该类还可以实现默认的处理行为：确定下个处理者存在后再将请求传递给它。

3.**具体处理者(Con­crete Han­dlers)** 包含处理请求的实际代码。每个处理者接收到请求后，都必须决定是否进行处理，以及是否沿着链传递请求。
处理者通常是独立且不可变的，需要通过构造函数一次性地获得所有必要地数据。

4.**客户端(Client)** 可根据程序逻辑一次性或者动态地生成链。值得注意的是，请求可发送给链上的任意一个处理者，而非必须是第一个处理者。

##### 伪代码

责任链在c#程序中并不常见，因为它仅在代码与对象链打交道时才能发挥作用。但是一旦用到这种链式请求，比如按顺序地验证答案，验证信息还是有用的。
在下段代码中，我们会给一批食物，让每个食物在责任链上走完，如果有动物要了，后续的链就会停止，如果会一直没有动物要，那就会返回 "{food} was left untouched"。那么，如果是信息验证的话，同理，我们让一个信息在链上走，如果中间有一步错了，马上停止，只有全部符合，才会报告信息验证成功。

```csharp
//Handler 接口声明了建立处理者链的的方法，也声明了执行请求的方法
public interface IHandler
{
    IHandler SetNext(IHandler handler);

    object Handle(object request);
}
//基础处理者类
public abstract class AbstractHandler : IHandler
{
    private IHandler _nextHandler;
    
    public IHandler SetNext(IHandler handler)
    {
        this._nextHandler = handler;

        return handler;
    }

    public virtual object Handle(object request)
    {
        if (this._nextHandler != null)
        {
            return this._nextHandler.Handle(request);
        }
        else
        {
            return null;
        }
    }
}
//具体处理者类
class MonkeyHandler : AbstractHandler
{
    public override object Handle(object request)
    {
        if ((request as string) == "Banana")
        {
            return $"Monkey: I'll eat the {request.ToString()}.\n";
        }
        else
        {
            return base.Handle(request);
        }
    }
}
class SquirrelHandler : AbstractHandler
{
    public override object Handle(object request)
    {
        if (request.ToString() == "Nut")
        {
            return $"Squirrel: I'll eat the {request.ToString()}.\n";
        }
        else
        {
            return base.Handle(request);
        }
    }
}
class DogHandler : AbstractHandler
{
    public override object Handle(object request)
    {
        if (request.ToString() == "MeatBall")
        {
            return $"Dog: I'll eat the {request.ToString()}.\n";
        }
        else
        {
            return base.Handle(request);
        }
    }
}
public class Client
{
    public static void ClientCode(AbstractHandler handler)
    {
        foreach (var food in new List<string> { "Nut", "Banana", "Cup of coffee" })
        {
            Console.WriteLine($"Client: Who wants a {food}?");

            var result = handler.Handle(food);

            if (result != null)
            {
                Console.Write($"   {result}");
            }
            else
            {
                Console.WriteLine($"   {food} was left untouched.");
            }
        }
    }
}

//客户端代码
var monkey = new MonkeyHandler();
var squirrel = new SquirrelHandler();
var dog = new DogHandler();

//设置责任链
monkey.setNext(squirrel).setNext(dog);

Console.WriteLine("Chain: Monkey > Squirrel > Dog\n");
Client.ClientCode(monkey);
Console.WriteLine();

Console.WriteLine("Subchain: Squirrel > Dog\n");
Client.ClientCode(squirrel);

/*运行结果
Chain: Monkey > Squirrel > Dog

Client: Who wants a Nut?
   Squirrel: I'll eat the Nut.
Client: Who wants a Banana?
   Monkey: I'll eat the Banana.
Client: Who wants a Cup of coffee?
   Cup of coffee was left untouched.

Subchain: Squirrel > Dog

Client: Who wants a Nut?
   Squirrel: I'll eat the Nut.
Client: Who wants a Banana?
   Banana was left untouched.
Client: Who wants a Cup of coffee?
   Cup of coffee was left untouched.
*/
```

##### 适合责任链模式的地方

- 当程序需要使用不同方式处理不同种类请求，而且请求类型和顺序预先未知时，可以使用责任链模式。
- 当必须按顺序执行多个处理者时，可以使用该模式。
- 如果所需处理者及其顺序必须在运行时进行改变， 可以使用责任链模式。

##### 责任链模式的优缺点

**优点** ：

- 你可以控制请求处理的顺序。
- 符合SRP
- 符合OCP

**缺点** ：

- 部分请求可能未被处理。

#### Command(命令模式)

命令模式是一种行为设计模式，它可将请求转换为一个包含与请求相关的所有信息的独立对象。该转换让你能根据不同的请求将方法参数化、延迟请求执行或将其放入队列中，且能实现可撤销操作。

##### 问题

假如你正在开发一款新的文字编辑器，当前的任务是创建一个包含多个按钮的工具栏，并让每个按钮对应编辑器的不同操作。你创建了一个非常简洁的按钮类，它不仅可用于生成工具栏上的按钮，还可用于生成各种对话框的通用按钮。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220824135308.png)

尽管所有按钮看上去都很相似，但它们可以完成不同的操作（打开、保存、打印和应用等）。你会在哪里放置这些按钮的点击处理代码呢？最简单的解决方案是在使用按钮的每个地方都创建大量的子类。这些子类中包含按钮点击后必须执行的代码。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220824135352.png)

你很快就意识到这种方式有严重缺陷。首先，你创建了大量的子类，当**每次修改基类按钮时,你都有可能需要修改所有子类的代码**。简单来说，GUI代码以一种拙劣的方式依赖于业务逻辑中的不稳定代码。

还有一个部分最难办。复制/粘贴文字等操作可能会在多个地方被调用。例如用户可以点击工具栏上小小的 “复制” 按钮，或者通过上下文菜单复制一些内容，又或者直接使用键盘上的 Ctrl+C 。

##### 解决方案

优秀的软件设计通常会将关注点进行分离，而这往往会导致软件的分层。最常见的例子：一层负责用户图像界面；另一层负责业务逻辑。GUI 层负责在屏幕上渲染美观的图形，捕获所有输入并显示用户和程序工作的结果。当需要完成一些重要内容时（比如计算月球轨道或撰写年度报告），GUI 层则会将工作委派给业务逻辑底层。
这在代码中看上去就像这样：一个 GUI 对象传递一些参数来调用一个业务逻辑对象。这个过程通常被描述为一个对象发送请求给另一个对象。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220824135547.png)

命令模式**建议 GUI 对象不直接提交这些请求**。你应该将**请求的所有细节** （例如调用的对象、 方法名称和参数列表） **抽取出来组成命令类**，该类中仅包含一个用于触发请求的方法。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220824135629.png)

下一步是让**所有命令实现相同的接口**。该接口通常只有一个没有任何参数的执行方法，让你能在不和具体命令类耦合的情况下使用同一请求发送者执行不同命令。此外还有额外的好处，现在你能在运行时切换连接至发送者的命令对象，以此改变发送者的行为。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220824135705.png)

##### 命令模式结构

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220824135728.png)

1.**发送者(Sender)——亦称 “触发者(Invok­er)”** 类负责对请求进行初始化，其中必须包含一个成员变量来存储对于命令对象的引用。发送者触发命令，而不向接收者直接发送请求。注意，发送者并不负责创建命令对象：它通常会通过构造函数从客户端处获得预先生成的命令。

2.**命令(Com­mand)** 接口通常仅声明一个执行命令的方法。

3.**具体命令(Con­crete Com­mands)** 会实现各种类型的请求。具体命令自身并不完成工作，而是会将调用委派给一个业务逻辑对象。但为了简化代码，这些类可以进行合并。
接收对象执行方法所需的参数可以声明为具体命令的成员变量。你可以将命令对象设为不可变，仅允许通过构造函数对这些成员变量进行初始化。

4.**接收者(Receiv­er)** 类包含部分业务逻辑。几乎任何对象都可以作为接收者。绝大部分命令只处理如何将请求传递到接收者的细节，接收者自己会完成实际的工作。

5.**客户端(Client)** 会创建并配置具体命令对象。 客户端必须将包括接收者实体在内的所有请求参数传递给命令的构造函数。此后，生成的命令就可以与一个或多个发送者相关联了。

##### 伪代码

命令模式十分常见。大部分情况下，它被用于代替包含行为的参数化 UI 元素的回调函数，此外还被用于对任务进行排序和记录操作历史记录等。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220824141646.png)

```csharp
//命令基类
public abstract class Command
{
    protected Application app;
    protected Editor editor;
    protected text backup;

    public Command(Application app,editor Editor)
    {
        this.app = app;
        this.editor = editor;
    }

    //备份编辑器状态
    public void saveBackup()
    {
        backup = editor.text;
    }

    //恢复编辑器状态
    public void undo()
    {
        editor.text = backup;
    }

    // 执行方法被声明为抽象以强制所有具体命令提供自己的实现。该方法必须根
    // 据命令是否更改编辑器的状态返回 true 或 false。
    public abstract bool execute();
}
//具体命令
public class CopyCommand : Command
{
    // 复制命令不会被保存到历史记录中，因为它没有改变编辑器的状态。
    public override bool execute()
    {
        app.clipboard = editor.getSelection();
        return false;
    }
}
public class CutCommand : Command
{
    // 剪切命令改变了编辑器的状态，因此它必须被保存到历史记录中。只要方法
    // 返回 true，它就会被保存。
    public override bool execute()
    {
        saveBackup();
        app.clipboard = editor.getSelection();
        editor.deleteSelection();
        return true;
    }
}
public class CutCommand : Command
{
    //粘贴命令改变了编辑器的状态
    // 返回 true，它就会被保存。
    public override bool execute()
    {
        saveBackup();
        editor.replaceSelection(app.clipboard);
        return true;
    }
}
public class UndoCommand : Command
{
    public override bool execute()
    {
        app.undo();
        return false;
    }
}
//全局命令历史记录就是一个堆栈
public class CommandHistory
{
    private Command[] history;

    public void push(Command c)
    {
        // 将命令压入历史记录数组的末尾。
    }
    public Command pop(Command c)
    {
        // 从历史记录中取出最近的命令。
    }
}
// 编辑器类包含实际的文本编辑操作。它会担任接收者的角色：最后所有命令都会
// 将执行工作委派给编辑器的方法。
public class Editor
{
    public string text;

    public string getSlection()
    {
        // 返回选中的文字。
    }

    public void deleteSelction()
    {
        // 删除选中的文字。
    }

    public void replaceSelection(string text)
    {
        // 在当前位置插入剪贴板中的内容。
    }
}
// 应用程序类会设置对象之间的关系。它会担任发送者的角色：当需要完成某些工
// 作时，它会创建并执行一个命令对象。
public class Application
{
    public string clipboard;
    public Editors[] editors;
    public Editor activeEditor;
    public CommandHistory histroy;

    //分发UI的命令
    public void createUI() 
    {
        //复制操作
        copy = function() { executeCommand(
            new CopyCommand(this, activeEditor)) };
        copyButton.setCommand(copy);
        shortcuts.onKeyPress("Ctrl+C", copy);

        //剪切操作
        cut = function() { executeCommand(
            new CutCommand(this, activeEditor)) };
        cutButton.setCommand(cut);
        shortcuts.onKeyPress("Ctrl+X", cut);

        //粘贴操作
        paste = function() { executeCommand(
            new PasteCommand(this, activeEditor)) };
        pasteButton.setCommand(paste);
        shortcuts.onKeyPress("Ctrl+V", paste);

        //撤销操作
        undo = function() { executeCommand(
            new UndoCommand(this, activeEditor)) };
        undoButton.setCommand(undo);
        shortcuts.onKeyPress("Ctrl+Z", undo);
    } 

    // 执行一个命令并检查它是否需要被添加到历史记录中。
    public void executeCommand(Command command)
    {
        if(command.execute)
        {
            history.push(command);
        }
    }

    // 从历史记录中取出最近的命令并运行其 undo（撤销）方法。请注意，你并
    // 不知晓该命令所属的类。但是我们不需要知晓，因为命令自己知道如何撤销
    // 其动作。
    public void undo()
    {
        Command command = history.pop();
        if(command != null) 
        {
            command.undo();
        }
    }
}
```

##### 适合命令模式的地方

- 如果你需要通过操作来参数化对象，可使用命令模式。
- 如果你想要将操作放入队列中、操作的执行或者远程执行操作，可使用命令模式。
- 如果你想要实现操作回滚功能，可使用命令模式。为了能够回滚操作，你需要实现已执行操作的历史记录功能。命令历史记录是一种包含所有已执行命令对象及其相关程序状态备份的栈结构。这种方法有两个缺点。首先，程序状态的保存功能并不容易实现，因为部分状态可能是私有的。你可以使用**备忘录模式**来在一定程度上解决这个问题。其次，备份状态可能会占用大量内存。因此，有时你需要借助另一种实现方式：命令无需恢复原始状态，而是执行反向操作。反向操作也有代价：它可能会很难甚至是无法实现。

##### 命令模式的优缺点 

**优点** :

- 符合SRP
- 符合OCP
- 你可以实现撤销和恢复功能。
- 你可以实现操作的延迟执行。
- 你可以将一组简单命令组合成一个复杂命令。

**缺点** :

- 代码可能会变得更加复杂，因为你在发送者和接收者之间增加了一个全新的层次。

#### Iterator(迭代器模式)

迭代器模式是一种行为设计模式，让你能在不暴露集合底层表现形式（列表、 栈和树等）的情况下遍历集合中所有的元素。

##### 问题

如果你的集合基于列表，那么这项工作听上去仿佛很简单。但如何遍历复杂数据结构（例如树）中的元素呢？例如，今天你需要使用深度优先算法来遍历树结构，明天可能会需要广度优先算法；下周则可能会需要其他方式 （比如随机存取树中的元素）。不断向集合中添加遍历算法会模糊其 “高效存储数据” 的主要职责。此外， 有些算法可能是根据特定应用订制的，将其加入泛型集合类中会显得非常奇怪。
另一方面，使用多种集合的客户端代码可能并不关心存储数据的方式。不过由于集合提供不同的元素访问方式，你的代码将不得不与特定集合类进行耦合。

##### 解决方案

迭代器模式的主要思想是将**集合的遍历行为抽取为单独的迭代器对象**。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220824153321.png)

除实现自身算法外，迭代器还封装了遍历操作的所有细节，例如当前位置和末尾剩余元素的数量。因此，多个迭代器可以在相互独立的情况下同时访问集合。
迭代器通常会提供一个获取集合元素的基本方法。客户端可不断调用该方法直至它不返回任何内容，这意味着迭代器已经遍历了所有元素。
所有迭代器必须实现相同的接口。这样一来，只要有合适的迭代器，客户端代码就能兼容任何类型的集合或遍历算法。如果你需要采用特殊方式来遍历集合，只需创建一个新的迭代器类即可，无需对集合或客户端进行修改。

##### 迭代器模式结构

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220824153429.png)

1.**迭代器(Iter­a­tor)** 接口声明了遍历集合所需的操作：获取下一个元素、获取当前位置和重新开始迭代等。

2.**具体迭代器(Con­crete Iter­a­tors)** 实现遍历集合的一种特定算法。迭代器对象必须跟踪自身遍历的进度。这使得多个迭代器可以相互独立地遍历同一集合。

3.**集合(Col­lec­tion)** 接口声明一个或多个方法来获取与集合兼容的迭代器。请注意，返回方法的类型必须被声明为迭代器接口，因此具体集合可以返回各种不同种类的迭代器。

4.**具体集合(Con­crete Col­lec­tions)** 会在客户端请求迭代器时返回一个特定的具体迭代器类实体。你可能会琢磨，剩下的集合代码在什么地方呢？不用担心，它也会在同一个类中。只是这些细节对于实际模式来说并不重要，所以我们将其省略了而已。

5.**客户端(Client)** 通过集合和迭代器的接口与两者进行交互。这样一来客户端无需与具体类进行耦合，允许同一客户端代码使用各种不同的集合和迭代器。
客户端通常不会自行创建迭代器，而是会从集合中获取。但在特定情况下，客户端可以直接创建一个迭代器（例如当客户端需要自定义特殊迭代器时）。

##### 伪代码

迭代器模式在c#中十分常见，基于IEnumerator和IEnumerable的使用，然后在foreach中就能很方便地实现。前者是计数器，后者是可计数的，也就相当于迭代器模式里的迭代器和集合

```csharp
//迭代器基类，实现IEnumerator接口
abstract class Iterator : IEnumerator
{
    object IEnumerator.Current => Current();

    // 返回当前元素的键
    public abstract int Key();    
    // 返回当前元素
    public abstract object Current();    
    // 移动到下一位元素
    public abstract bool MoveNext();    
    // 重置当前指的位置到初始位置
    public abstract void Reset();
}
//集合基类
abstract class IteratorAggregate : Ienumerable
{
    //返回集合对应的迭代器
    public abstract IEnumerator GetEnumerator();
}
//具体迭代器的遍历算法
class AlphabeticalOrderIterator : Iterator
{
    private WordsCollection _collection;

    private int _position = -1;

    private bool _reverse = false;
    public AlphabeticalOrderIterator(WordsCollection collection, bool reverse = false)
    {
        this._collection = collection;
        this._reverse = reverse;
        if (reverse)
        {
            this._position = collection.getItems().Count;
        }
    }

    public override int Key()
    {
        return this._position;
    }

    public override object Current()
    {
        return this._collection.getItems()[_position];
    }

    public override bool MoveNext()
    {
        int updatedPosition = this._position + (this._reverse ? -1 : 1);

        if(updatedPosition >= 0 && updatedPosition < this._collection.getItems())
        {
            this._position = updatePosition;
            return true;
        }
        else 
        {
            return false;
        }
    }

    public override void Reset()
    {
        this._position = this._reverse ? this._collection.getItems().Count - 1 : 0;
    }
}
//具体集合类
class WordsCollection : IteratorAggregate
{
    List<string> _collection = new List<string>();
    
    //决定是否反转
    bool _direction = false;
        
    public void ReverseDirection()
    {
        _direction = !_direction;
    }
        
    public List<string> getItems()
    {
        return _collection;
    }
        
    public void AddItem(string item)
    {
        this._collection.Add(item);
    }
        
    public override IEnumerator GetEnumerator()
    {
        return new AlphabeticalOrderIterator(this, _direction);
    }
}

//客户端代码
var collection = new WordsCollection();
collection.AddItem("First");        collection.AddItem("Second");        collection.AddItem("Third");
Console.WriteLine("Straight traversal:");

foreach (var element in collection)
{
    Console.WriteLine(element);
}

Console.WriteLine("\nReverse traversal:");

collection.ReverseDirection();

foreach (var element in collection)
{
    Console.WriteLine(element);
}

/*运行结果
Straight traversal:
First
Second
Third

Reverse traversal:
Third
Second
First
*/
```

##### 适合迭代器模式的地方

- 当集合背后为复杂的数据结构，且你希望对客户端隐藏其复杂性时（出于使用便利性或安全性的考虑），可以使用迭代器模式。
- 使用该模式可以减少程序中重复的遍历代码。
- 如果你希望代码能够遍历不同的甚至是无法预知的数据结构，可以使用迭代器模式。

##### 迭代器模式的优缺点

**优点** :

- 符合SRP
- 符合OCP
- 你可以并行遍历同一集合，因为每个迭代器对象都包含其自身的遍历状态。
- 相似的，你可以暂停遍历并在需要时继续。

**缺点** :

- 如果你的程序只与简单的集合进行交互，应用该模式可能会矫枉过正。
- 对于某些特殊集合，使用迭代器可能比直接遍历的效率低。

#### Mediator(中介者模式)

中介者模式是一种行为设计模式，能让你减少对象之间混乱无序的依赖关系。该模式会限制对象之间的直接交互，迫使它们通过一个中介者对象进行合作。

##### 问题

假如你有一个创建和修改客户资料的对话框，它由各种控件组成，例如文本框（Text­Field）、复选框 （Check­box）和按钮（But­ton）等。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220824213630.png)

如果直接在表单元素代码中实现业务逻辑，你将很难在程序其他表单中复用这些元素类。例如，由于复选框类与狗狗的文本框相耦合，所以将无法在其他表单中使用它。你要么使用渲染资料表单时用到的所有类，要么一个都不用。

##### 解决方案

中介者模式建议你**停止组件之间的直接交流并使其相互独立**。这些组件必须调用特殊的中介者对象，通过中介者对象重定向调用行为，以间接的方式进行合作。最终，**组件仅依赖于一个中介者类，无需与多个其他组件相耦合**。
你还可以为所有类型的对话框抽取通用接口，进一步削弱其依赖性。接口中将声明一个所有表单元素都能使用的通知方法，可用于将元素中发生的事件通知给对话框。这样一来，所有实现了该接口的对话框都能使用这个提交按钮了。
采用这种方式，中介者模式让你能在单个中介者对象中封装多个对象间的复杂关系网。类所拥有的依赖关系越少，就越易于修改、扩展或复用。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220824213818.png)

飞行器驾驶员们在靠近或离开空中管制区域时不会直接相互交流。但他们会与飞机跑道附近，塔台中的空管员通话。如果没有空管员，驾驶员就需要留意机场附近的所有飞机，并与数十位飞行员组成的委员会讨论降落顺序。那恐怕会让飞机坠毁的统计数据一飞冲天吧。

塔台无需管制飞行全程，只需在航站区加强管控即可，因为该区域的决策参与者数量对于飞行员来说实在太多了。

##### 中介者模式结构

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220824213846.png)

1.**组件(Com­po­nent)** 是各种包含业务逻辑的类。每个组件都有一个指向中介者的引用，该引用被声明为中介者接口类型。组件不知道中介者实际所属的类，因此你可通过将其连接到不同的中介者以使其能在其他程序中复用。

2.**中介者(Medi­a­tor)** 接口声明了与组件交流的方法，但通常仅包括一个通知方法。组件可将任意上下文（包括自己的对象）作为该方法的参数，只有这样接收组件和发送者类之间才不会耦合。

3.**具体中介者(Con­crete Medi­a­tor)** 封装了多种组件间的关系。具体中介者通常会保存所有组件的引用并对其进行管理，甚至有时会对其生命周期进行管理。

4.组件并不知道其他组件的情况。如果组件内发生了重要事件，它只能通知中介者。中介者收到通知后能轻易地确定发送者，这或许已足以判断接下来需要触发的组件了。
对于组件来说，中介者看上去完全就是一个黑箱。发送者不知道最终会由谁来处理自己的请求，接收者也不知道最初是谁发出了请求。

##### 伪代码

中介者模式在 C# 代码中最常用于帮助程序 GUI 组件之间的通信。在 MVC 模式中，控制器是中介者的同义词。

```csharp
//中介者接口声明各种元素通过活动相互通知的方法
public interface IMediator
{
    void Notify(object sender,string ev);
}
//具体中介者
class ConcreteMediator : IMediator
{
    private Component1 _component1;
    private Component2 _component2;

    public ConcreteMediator(Component1 component1, Component2 component2)
    {
        this._component1 = component1;
        this._component1.SetMediator(this);
        this._component2 = component2;
        this._component2.SetMediator(this);
    }

    public void Notify(object sender,string ev)
    {
        if (ev == "A")
        {
            Console.WriteLine("Mediator reacts on A and triggers folowing operations:");
            this._component2.DoC();
        }
        if (ev == "D")
        {
            Console.WriteLine("Mediator reacts on D and triggers following operations:");                
            this._component1.DoB();
            this._component2.DoC();
        }        
    }
}

//基本组件类提供存储对应的引用的中介者的功能
class BaseComponent
{
    protected IMediator _mediator;

    public BaseComponent(IMediator mediator =null)
    {
        this._mediator = mediator;
    }

    public void SetMediator(IMediator mediator)
    {
        this._mediator = mediator;
    }
}
//具体组件实现具体功能，不同的具体组件虽然
//会相互用到，但并不会直接用到，只会通过
//中介者来引用
class Component1 : BaseComponent
{
    public void DoA()
    {
        Console.WriteLine("Component 1 does A.");

        this._mediator.Notify(this,"A");
    }
    public void DoB()
    {
        Console.WriteLine("Component 1 does B.");

        this._mediator.Notify(this, "B");
    }
}
class Component2 : BaseComponent
{
    public void DoC()
    {
        Console.WriteLine("Component 2 does C.");

        this._mediator.Notify(this, "C");
    }
    public void DoD()
    {
        Console.WriteLine("Component 2 does D.");

        this._mediator.Notify(this, "D");
    }
}

//客户端代码
Component1 component1 = new Component1();
Component2 component2 = new Component2();
new ConcreteMediator(component1, component2);

Console.WriteLine("Client triggets operation A.");
component1.DoA();

Console.WriteLine();

Console.WriteLine("Client triggers operation D.");
component2.DoD();

/*运行结果
Client triggers operation A.
Component 1 does A.
Mediator reacts on A and triggers following operations:
Component 2 does C.

Client triggers operation D.
Component 2 does D.
Mediator reacts on D and triggers following operations:
Component 1 does B.
Component 2 does C.
*/
```

##### 适合中介者模式的地方

- 当一些对象和其他对象紧密耦合以致难以对其进行修改时，可使用中介者模式。
- 当组件因过于依赖其他组件而无法在不同应用中复用时，可使用中介者模式。
- 如果为了能在不同情景下复用一些基本行为，导致你需要被迫创建大量组件子类时，可使用中介者模式。

##### 中介者模式的优缺点

**优点** ：

- 符合SRP
- 符合OCP
- 你可以减轻应用中多个组件间的耦合情况。
- 你可以更方便地复用各个组件。

**缺点** ：

- 一段时间后，中介者可能会演化成为上帝对象。

#### Memento(备忘录模式)

备忘录模式是一种行为设计模式，允许在不暴露对象实现细节的情况下保存和恢复对象之前的状态。

##### 问题

假如你正在开发一款文字编辑器应用程序。除了简单的文字编辑功能外，编辑器中还要有设置文本格式和插入内嵌图片等功能。
后来，你决定让用户能撤销施加在文本上的任何操作。这项功能在过去几年里变得十分普遍，因此用户期待任何程序都有这项功能。你选择采用直接的方式来实现该功能：程序在执行任何操作前会记录所有的对象状态，并将其保存下来。当用户此后需要撤销某个操作时，程序将从历史记录中获取最近的快照，然后使用它来恢复所有对象的状态。
让我们来思考一下这些状态快照。首先，到底该如何生成一个快照呢？很可能你会需要遍历对象的所有成员变量并将其数值复制保存。但只有当对象对其内容没有严格访问权限限制的情况下，你才能使用该方式。不过很遗憾，绝大部分对象会使用私有成员变量来存储重要数据，这样别人就无法轻易查看其中的内容。
现在我们暂时忽略这个问题，假设对象都像嬉皮士一样：喜欢开放式的关系并会公开其所有状态。尽管这种方式能够解决当前问题，让你可随时生成对象的状态快照，但这种方式仍存在一些严重问题。未来你可能会添加或删除一些成员变量。这听上去很简单，但需要对负责复制受影响对象状态的类进行更改。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220825143929.png)

还有更多问题。让我们来考虑编辑器 （Edi­tor）状态的实际 “快照”，它需要包含哪些数据？至少必须包含实际的文本、光标坐标和当前滚动条位置等。你需要收集这些数据并将其放入特定容器中，才能生成快照。
你很可能会将大量的容器对象存储在历史记录列表中。这样一来，容器最终大概率会成为同一个类的对象。这个类中几乎没有任何方法，但有许多与编辑器状态一一对应的成员变量。为了让其他对象能保存或读取快照，你很可能需要将快照的成员变量设为公有。无论这些状态是否私有，其都将暴露一切编辑器状态。其他类会对快照类的每个小改动产生依赖，除非这些改动仅存在于私有成员变量或方法中，而不会影响外部类。
我们似乎走进了一条死胡同：**要么会暴露类的所有内部细节而使其过于脆弱；要么会限制对其状态的访问权限而无法生成快照**。那么，我们还有其他方式来实现 “撤销” 功能吗？

##### 解决方案

我们刚才遇到的所有问题都是封装 “破损” 造成的。 一些对象试图超出其职责范围的工作。由于在执行某些行为时需要获取数据，所以它们侵入了其他对象的私有空间，而不是让这些对象来完成实际的工作。

备忘录模式将创建状态快照（Snap­shot）的工作委派给实际状态的拥有者原发器 （Orig­i­na­tor） 对象。这样其他对象就不再需要从 “外部” 复制编辑器状态了，编辑器类拥有其状态的完全访问权，因此可以自行生成快照。

模式建议将对象状态的副本存储在一个名为备忘录 （Memen­to）的特殊对象中。除了创建备忘录的对象外，任何对象都不能访问备忘录的内容。其他对象必须使用受限接口与备忘录进行交互，它们可以获取快照的元数据 （创建时间和操作名称等），但不能获取快照中原始对象的状态。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220825144342.png)

这种限制策略允许你将备忘录保存在通常被称为负责人（Care­tak­ers）的对象中。由于负责人仅通过受限接口与备忘录互动，故其无法修改存储在备忘录内部的状态。同时，原发器拥有对备忘录所有成员的访问权限，从而能随时恢复其以前的状态。

在文字编辑器的示例中，我们可以创建一个独立的历史 （His­to­ry） 类作为负责人。编辑器每次执行操作前，存储在负责人中的备忘录栈都会生长。你甚至可以在应用的 UI 中渲染该栈，为用户显示之前的操作历史。

当用户触发撤销操作时，历史类将从栈中取回最近的备忘录，并将其传递给编辑器以请求进行回滚。由于编辑器拥有对备忘录的完全访问权限，因此它可以使用从备忘录中获取的数值来替换自身的状态。

##### 备忘录模式结构

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220825144517.png)

1.**原发器(Orig­i­na­tor)** 类可以生成自身状态的快照，也可以在需要时通过快照恢复自身状态。

2.**备忘录(Memen­to)** 是原发器状态快照的值对象(value object)。通常做法是将备忘录设为不可变的， 并通过构造函数一次性传递数据。

3.**负责人(Care­tak­er)** 仅知道 “何时” 和 “为何” 捕捉原发器的状态，以及何时恢复状态。
负责人通过保存备忘录栈来记录原发器的历史状态。 当原发器需要回溯历史状态时，负责人将从栈中获取最顶部的备忘录，并将其传递给原发器的恢复 (restora­tion)方法。

4.在该实现方法中，备忘录类将被嵌套在原发器中。 这样原发器就可访问备忘录的成员变量和方法，即使这些方法被声明为私有。另一方面，负责人对于备忘录的成员变量和方法的访问权限非常有限：它们只能在栈中保存备忘录，而不能修改其状态。

##### 伪代码

备忘录的基本功能可用序列化来实现，这在 C# 语言中很常见。尽管备忘录不是生成对象状态快照的唯一或最有效的方法，但它能在保护原始对象的结构不暴露给其他对象的情况下保存对象状态的备份。在游戏中，比如地平线的回退，PBUG的死亡回放等等都可能是用到了备忘录模式。
这个模式还是有点复杂的，仅仅通过结构不太能区分Originator和Caretaker，通过代码来简单了解一下。

简单谈一下之后的伪代码，这次的结构比较复杂，所以建议最好运行一遍然后看懂代码，简单来说就是Caretaker负责做，通过Caretaker类来使Originator创建一次Memento然后存储到Caretaker里的list。如果是撤回之前的状态，同样用Caretaker的Undo来触发Originator的Restore函数。也就是说，Caretaker是发起者，Originator是Memento的创造者，Memento只是用来存储一次的状态。

```csharp
//Originator类会存储一些重要的可能会随时间改变的状态。同时也定义了保存和存储状态的方法
class Originator
{
    //在伪代码中尽量简单，这里只用了string类型
    private string _state;

    public Originator(string state)
    {
        this._state = state;
        Console.WriteLine("Originator: My initial state is: " + state);
    }

    //这里的
    public void DoSomething()
    {
        Console.WriteLine("Originator: I'm doing something important.");
        this._state = this.GenerateRandomString(30);
        Console.WriteLine($"Originator: and my state has changed to: {_state}");
    }

    //通过时间生成随机的字符串
    private string GenerateRandomString(int length = 10)
    {
        string allowedSymbols = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";
        string result = string.Empty;

        while (length > 0)
        {
            result += allowedSymbols[new Random().Next(0, allowedSymbols.Length)];

            Thread.Sleep(12);

            length--;
        }
        return result;
    }

    //保存现在的状态
    public IMemento Save()
    {
        return new ConcreteMemento(this._state);
    }

    //恢复之前的状态
    public void Restore(IMemento memento)
    {
        if(!(memento is ConcreteMemento))
        {
            throw new Exception("Unknown memento class " + memento.ToString());
        }

        this._state = memento.GetState();
        Console.Write($"Originator: My state has changed to: {_state}");
    }
}
//备忘录接口
public interface IMemento
{
    string GetName();

    string GetState();

    DateTime GetDate();
}
//具体备忘录
class ConcreteMemento : IMemento
{
    private string _state;

    private DateTime _date;

    public ConcreteMemento(string state)
    {
        this._state = state;
        this._date = DateTime.Now;
    }

    public string GetState()
    {
        return this._state;
    }
    public string GetName()
    {
        return $"{this._date} / ({this._state.Substring(0, 9)})...";
    }

    public DateTime GetDate()
    {
        return this._date;
    }
}
class Caretaker
{
    private List<IMemento> _mementos = new List<IMemento>();

    private Originator _originator = null;

     public Caretaker(Originator originator)
    {
        this._originator = originator;
    }

    //备份
    public void Backup()
    {
        Console.WriteLine("\nCaretaker: Saving Originator's state...");
        this._mementos.Add(this._originator.Save());
    }

    //撤销
    public void Undo()
    {
        if (this._mementos.Count == 0)
        {
            return;
        }

        var memento = this._mementos.Last();
        this._mementos.Remove(memento);

        Console.WriteLine("Caretaker: Restoring state to: " + memento.GetName());

        try
        {
            this._originator.Restore(memento);
        }
        catch (Exception)
        {
            this.Undo();
        }
    }

    public void ShowHistory()
    {
        Console.WriteLine("Caretaker: Here's the list of mementos:");

        foreach (var memento in this._mementos)
        {
            Console.WriteLine(memento.GetName());
        }
    }
}

//客户端代码
Originator originator = new Originator("Super-duper-super-puper-super.");
Caretaker caretaker = new Caretaker(originator);

caretaker.Backup();
originator.DoSomething();

caretaker.Backup();
originator.DoSomething();

caretaker.Backup();
originator.DoSomething();

Console.WriteLine();
caretaker.ShowHistory();

Console.WriteLine("\nClient: Now, let's rollback!\n");
caretaker.Undo();

Console.WriteLine("\n\nClient: Once more!\n");
caretaker.Undo();

Console.WriteLine();

/*运行结果,根据当前时间有所变化
可以更改客户端代码来体会更深

Originator: My initial state is: Super-duper-super-puper-super.

Caretaker: Saving Originator's state...
Originator: I'm doing something important.
Originator: and my state has changed to: oGyQIIatlDDWNgYYqJATTmdwnnGZQj

Caretaker: Saving Originator's state...
Originator: I'm doing something important.
Originator: and my state has changed to: jBtMDDWogzzRJbTTmEwOOhZrjjBULe

Caretaker: Saving Originator's state...
Originator: I'm doing something important.
Originator: and my state has changed to: exoHyyRkbuuNEXOhhArKccUmexPPHZ

Caretaker: Here's the list of mementos:
12.06.2018 15:52:45 / (Super-dup...)
12.06.2018 15:52:46 / (oGyQIIatl...)
12.06.2018 15:52:46 / (jBtMDDWog...)

Client: Now, let's rollback!

Caretaker: Restoring state to: 12.06.2018 15:52:46 / (jBtMDDWog...)
Originator: My state has changed to: jBtMDDWogzzRJbTTmEwOOhZrjjBULe

Client: Once more!

Caretaker: Restoring state to: 12.06.2018 15:52:46 / (oGyQIIatl...)
Originator: My state has changed to: oGyQIIatlDDWNgYYqJATTmdwnnGZQj
*/
```

##### 适合备忘录模式的地方

- 当你需要创建对象状态快照来恢复其之前的状态时，可以使用备忘录模式。
- 当直接访问对象的成员变量、获取器或设置器将导致封装被突破时，可以使用该模式。

##### 备忘录模式的优缺点

**优点** ：

- 你可以在不破坏对象封装情况的前提下创建对象状态快照。
- 你可以通过让负责人维护原发器状态历史记录来简化原发器代码。

**缺点** ：

- 如果客户端过于频繁地创建备忘录，程序将消耗大量内存。
- 负责人必须完整跟踪原发器的生命周期，这样才能销毁弃用的备忘录。
- 绝大部分动态编程语言 （例如 PHP、 Python 和 JavaScript） 不能确保备忘录中的状态不被修改（与c#关系不大）。

#### Observer(观察者模式)

观察者模式是一种行为设计模式，允许你定义一种订阅机制，可在对象事件发生时通知多个 “观察” 该对象的其他对象。

##### 问题

假如你有两种类型的对象：​顾客和 商店 。顾客对某个特定品牌的产品非常感兴趣（例如最新型号的 iPhone 手机），而该产品很快将会在商店里出售。
顾客可以每天来商店看看产品是否到货。但如果商品尚未到货时，绝大多数来到商店的顾客都会空手而归。另一方面，每次新产品到货时，商店可以向所有顾客发送邮件（可能会被视为垃圾邮件）。这样，部分顾客就无需反复前往商店了，但也可能会惹恼对新产品没有兴趣的其他顾客。
我们似乎遇到了一个矛盾：要么让顾客浪费时间检查产品是否到货，要么让商店浪费资源去通知没有需求的顾客。

##### 解决方案

拥有一些值得关注的状态的对象通常被称为目标，由于它要**将自身的状态改变通知给其他对象**，我们也将其称为发布者(pub­lish­er)。所有**希望关注发布者状态变化的其他对象**被称为订阅者(sub­scribers)。

观察者模式建议你为发布者类添加订阅机制，让每个对象都能订阅或取消订阅发布者事件流。不要害怕！这并不像听上去那么复杂。实际上，该机制包括 **1)** 一个用于存储订阅者对象引用的列表成员变量；**2)** 几个用于添加或删除该列表中订阅者的公有方法。

如果你的应用中有多个不同类型的发布者，且希望订阅者可兼容所有发布者，那么你甚至可以进一步让所有发布者遵循同样的接口。该接口仅需描述几个订阅方法即可。这样订阅者就能在不与具体发布者类耦合的情况下通过接口观察发布者的状态。

##### 观察者模式结构

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220825160617.png)

1.**发布者(Pub­lish­er)** 会向其他对象发送值得关注的事件。事件会在发布者自身状态改变或执行特定行为后发生。发布者中包含一个允许新订阅者加入和当前订阅者离开列表的订阅构架。

2.当新事件发生时，发送者会遍历订阅列表并调用每个订阅者对象的通知方法。该方法是在订阅者接口中声明的。

3.**订阅者(Sub­scriber)** 接口声明了通知接口。在绝大多数情况下，该接口仅包含一个 update更新方法。该方法可以拥有多个参数，使发布者能在更新时传递事件的详细信息。

4.**具体订阅者(Con­crete Sub­scribers)** 可以执行一些操作来回应发布者的通知。所有具体订阅者类都实现了同样的接口，因此发布者不需要与具体类相耦合。

5.订阅者通常需要一些上下文信息来正确地处理更新。因此，发布者通常会将一些上下文数据作为通知方法的参数进行传递。发布者也可将自身作为参数进行传递，使订阅者直接获取所需的数据。

6.**客户端(Client)** 会分别创建发布者和订阅者对象，然后为订阅者注册发布者更新。

##### 伪代码

观察者模式在 C# 代码中很常见，特别是在 GUI 组件中。它提供了在不与其他对象所属类耦合的情况下对其事件做出反应的方式。只要是一对多的广播模式的需求，观察者模式基本上可以用到。而且代码结构十分容易理解

```csharp
//提供订阅者接口
public interface ISubscriber
{
    //添加Observer，也就是接受信息的人
    void Attach(IObserver observer);

    //去掉Observer
    void Detach(IObserver observer);

    //通知
    void Notify();
}
//发布者拥有自身状态
public class Subscriber : ISubscriber
{
    //当发布器状态发生改变的时候可能要进行推送
    //伪代码这里简化了状态
    public int State {get;set;} = -0;

    //订阅发布器的队列
    private List<IObserver> _observers = new List<IObserver>();

    public void Attach(IObserver observer)
    {
        Console.WriteLine("Subscriber: Attached an obseerver.");
        this._observers.Add(observer);
    }

    public void Detach(IObserver observer)
    {
        this._observers.Remove(observer);
        Console.WriteLine("Subscriber: Detached an observer.");
    }

    public void Notify()
    {
        Console.WriteLine("Subscriber: Notifying observers...");

        foreach (var observer in _observers)
        {
            observer.Update(this);
        }
    }

    //主要的业务逻辑
    public void SomeBusinessLogic()
    {
        Console.WriteLine("\nsubscriber: I'm doing something important.");
        this.State = new Random().Next(0, 10);

        Thread.Sleep(15);

        Console.WriteLine("subscriber: My state has just changed to: " + this.State);
        this.Notify();
    }
}
//通用观察者接口
public interface IObserver
{
    void Update(ISubscriber subscriber);
}
//具体观察者
class ConcreteObserverA : IObserver
{
    public void Update(ISubscriber subscriber)
    {            
        if ((subscriber as Subscriber).State < 3)
        {
            Console.WriteLine("ConcreteObserverA: Reacted to the event.");
        }
    }
}
class ConcreteObserverB : IObserver
{
    public void Update(ISubscriber subscriber)
    {
        if ((subscriber as Subscriber).State == 0 || (subscriber as Subscriber).State >= 2)
        {
            Console.WriteLine("ConcreteObserverB: Reacted to the event.");
        }
    }
}

//客户端代码
var subscriber = new Subscriber();

var observerA = new ConcreteObserverA();
subscriber.Attach(observerA);

var observerB = new ConcreteObserverB();
subscriber.Attach(observerB);

subscriber.SomeBusinessLogic();
subscriber.SomeBusinessLogic();

subscriber.Detach(observerB);

subscriber.SomeBusinessLogic();

/*运行结果
Subscriber: Attached an observer.
Subscriber: Attached an observer.

Subscriber: I'm doing something important.
Subscriber: My state has just changed to: 2
Subscriber: Notifying observers...
ConcreteObserverA: Reacted to the event.
ConcreteObserverB: Reacted to the event.

Subscriber: I'm doing something important.
Subscriber: My state has just changed to: 1
Subscriber: Notifying observers...
ConcreteObserverA: Reacted to the event.
Subscriber: Detached an observer.

Subscriber: I'm doing something important.
Subscriber: My state has just changed to: 5
Subscriber: Notifying observers...
*/
```

##### 适合观察者模式的地方

- 当一个对象状态的改变需要改变其他对象，或实际对象是事先未知的或动态变化的时，可使用观察者模式。
- 当应用中的一些对象必须观察其他对象时，可使用该模式。但仅能在有限时间内或特定情况下使用。

##### 观察者模式的优缺点

**优点** ：

- 符合OCP
- 你可以在运行时建立对象之间的联系。


**缺点** ：

- 订阅者的通知顺序是随机的。

#### State(状态模式)

状态模式是一种行为设计模式，让你能在一个对象的内部状态变化时改变其行为，使其看上去就像改变了自身所属的类一样。

##### 问题

状态模式与有限状态机的概念紧密相关。
其主要思想是程序在任意时刻仅可处于几种**有限的状态**中。在任何一个特定状态中，程序的行为都不相同，且可瞬间从一个状态切换到另一个状态。不过，根据当前状态，程序可能会切换到另外一种状态，也可能会保持当前状态不变。这些数量有限且预先定义的状态切换规则被称为转移。

状态机通常由众多条件运算符 （ if或 switch ） 实现，可根据对象的当前状态选择相应的行为。 ​“状态” 通常只是对象中的一组成员变量值。即使你之前从未听说过有限状态机，你也很可能已经实现过状态模式。下面的代码应该能帮助你回忆起来。

```csharp
class Document is
    field state: string
    // ...
    method publish() is
        switch (state)
            "draft":
                state = "moderation"
                break
            "moderation":
                if (currentUser.role == "admin")
                    state = "published"
                break
            "published":
                // 什么也不做。
                break
    // ...
```

当我们逐步在文档类中添加更多状态和依赖于状态的行为后，基于条件语句的状态机就会暴露其最大的弱点。为了能根据当前状态选择完成相应行为的方法，绝大部分方法中会包含复杂的条件语句。修改其转换逻辑可能会涉及到修改所有方法中的状态条件语句，导致代码的维护工作非常艰难。

##### 解决方案

状态模式建议为对象的所有可能状态新建一个类，然后将所有状态的对应行为抽取到这些类中。

原始对象被称为上下文(con­text)，它并不会自行实现所有行为，而是会保存一个指向表示当前状态的状态对象的引用，且将所有与状态相关的工作委派给该对象。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220825164123.png)

如需将上下文转换为另外一种状态，则需将当前活动的状态对象替换为另外一个代表新状态的对象。采用这种方式是有前提的：所有状态类都必须遵循同样的接口，而且上下文必须仅通过接口与这些对象进行交互。

这个结构可能看上去与策略模式相似，但有一个关键性的不同—— 在状态模式中，特**定状态知道其他所有状态的存在，且能触发从一个状态到另一个状态的转换**；策略则**几乎完全不知道其他策略的存在**。

##### 状态模式结构

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220825164235.png)

1.**上下文(Con­text)** 保存了对于一个具体状态对象的引用，并会将所有与该状态相关的工作委派给它。上下文通过状态接口与状态对象交互，且会提供一个设置器用于传递新的状态对象。

2.**状态(State)** 接口会声明特定于状态的方法。这些方法应能被其他所有具体状态所理解，因为你不希望某些状态所拥有的方法永远不会被调用。

3.**具体状态(Con­crete States)** 会自行实现特定于状态的方法。为了避免多个状态中包含相似代码，你可以提供一个封装有部分通用行为的中间抽象类。
状态对象可存储对于上下文对象的反向引用。状态可以通过该引用从上下文处获取所需信息，并且能触发状态转移。

4.上下文和具体状态都可以设置上下文的下个状态，并可通过替换连接到上下文的状态对象来完成实际的状态转换。

##### 伪代码

状态模式在游戏中还是十分常见的，比如人物动画状态的变化，但是比较多的还是AI中，不过是简单游戏里的（大型游戏的方案可能不太一样）

```csharp
//Context类就是要进行状态变化的类
class Context
{
    private State _state = null;

    public Context(State state)
    {
        this.ChangeState(state);
    }

    public void ChangeState(State state)
    {
        Console.WriteLine($"Context: Transition to {state.GetType().Name}.");
        this._state = state;
        this._state.SetContext(this);
    }

    public void Request1()
    {
        this._state.Handle1();
    }

    public void Request2()
    {
        this._state.Handle2();
    }
}
//状态基类
abstract class State
{
    protected Context _context;

    public void SetContext(Context context)
    {
        this._context = context;
    }

    public abstract void Handle1();

    public abstract void Handle2();
}
class ConcreteStateA : State
{
    public override void Handle1()
    {
       Console.WriteLine("ConcreteStateA handles request1.");
        Console.WriteLine("ConcreteStateA wants to change the state of the context.");
       this._context.ChangeState(new ConcreteStateB());
    }

    public override void Handle2()
    {
       Console.WriteLine("ConcreteStateA handles request2.");
    }
}
class ConcreteStateB : State
{
    public override void Handle1()
    {
        Console.Write("ConcreteStateB handles request1.");
    }

    public override void Handle2()
    {
        Console.WriteLine("ConcreteStateB handles request2.");
        Console.WriteLine("ConcreteStateB wants to change the state of the context.");
        this._context.ChangeState(new ConcreteStateA());
    }
}

//客户端代码
var context = new Context(new ConcreteStateA());
context.Request1();
context.Request2();

/*运行结果
Context: Transition to ConcreteStateA.
ConcreteStateA handles request1.
ConcreteStateA wants to change the state of the context.
Context: Transition to ConcreteStateB.
ConcreteStateB handles request2.
ConcreteStateB wants to change the state of the context.
Context: Transition to ConcreteStateA.
*/
```

##### 适合状态模式的地方

- 如果对象需要根据自身当前状态进行不同行为，同时状态的数量非常多且与状态相关的代码会频繁变更的话，可使用状态模式。
- 如果某个类需要根据成员变量的当前值改变自身行为，从而需要使用大量的条件语句时，可使用该模式。
- 当相似状态和基于条件的状态机转换中存在许多重复代码时，可使用状态模式。

##### 状态模式的优缺点

**优点** ：

- 符合SRP
- 符合OCP
- 通过消除臃肿的状态机条件语句简化上下文代码。

**缺点** ：

- 如果状态机只有很少的几个状态，或者很少发生改变，那么应用该模式可能会显得小题大作。

#### Strategy(策略模式)

策略模式是一种行为设计模式，它能让你定义一系列算法，并将每种算法分别放入独立的类中，以使算法的对象能够相互替换。

##### 问题

一天，你打算为游客们创建一款导游程序。该程序的核心功能是提供美观的地图， 以帮助用户在任何城市中快速定位。用户期待的程序新功能是自动路线规划：他们希望输入地址后就能在地图上看到前往目的地的最快路线。程序的首个版本只能规划公路路线。驾车旅行的人们对此非常满意。但很显然，并非所有人都会在度假时开车。因此你在下次更新时添加了规划步行路线的功能。此后，你又添加了规划公共交通路线的功能。而这只是个开始。不久后，你又要为骑行者规划路线。又过了一段时间，你又要为游览城市中的所有景点规划路线。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220826203722.png)

##### 解决方案

策略模式建议**找出负责用许多不同方式完成特定任务的类，然后将其中的算法抽取到一组**被称为策略的独立类中。名为上下文的原始类必须包含一个成员变量来存储对于每种策略的引用。上下文并不执行任务，而是将工作委派给已连接的策略对象。上下文不负责选择符合任务需要的算法——客户端会将所需策略传递给上下文。实际上，上下文并不十分了解策略，它会通过同样的通用接口与所有策略进行交互，而该接口只需暴露一个方法来触发所选策略中封装的算法即可。（上下文其实就是主角）

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220826205036.png)

##### 策略模式结构

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220826205148.png)

1.**上下文(Con­text)** 维护指向具体策略的引用，且仅通过策略接口与该对象进行交流。

2.**策略(Strat­e­gy)** 接口是所有具体策略的通用接口，它声明了一个上下文用于执行策略的方法。

3.**具体策略(Con­crete Strate­gies)** 实现了上下文所用算法的各种不同变体。

4.当上下文需要运行算法时，它会在其已连接的策略对象上调用执行方法。上下文不清楚其所涉及的策略类型与算法的执行方式。

5.**客户端(Client)** 会创建一个特定策略对象并将其传递给上下文。上下文则会提供一个设置器以便客户端在运行时替换相关联的策略。

##### 伪代码

由于跟状态模式很相近，还是很容易理解的，注意一下不同就可以。

```csharp
//Context主体类，其实可以是Player类，相当于主题做操作的类
class Context
{
    //使用的策略
    private IStrategy _strategy;

    public Context() {}

    public Context(IStrategy strategy)
    {
        this._strategy = strategy;
    }

    public void SetStrategy(IStrategy strategy)
    {
        this._strategy = strategy;
    }

    //根据策略进行操作
    public void DoSomeBusinessLogic()
    {
        Console.WriteLine("Context: Sorting data using the strategy (not sure how it'll do it)");
        var result = this._strategy.DoAlgorithm(new List<string> { "a", "b", "c", "d", "e" });

        string resultStr = string.Empty;
        foreach (var element in result as List<string>)
        {
            resultStr += element + ",";
        }

        Console.WriteLine(resultStr);
    }
}
//Strategy接口声明方法
public interface IStrategy
{
    object DoAlgorithm(object data);
}
//具体策略
class ConcreteStrategyA : IStrategy
{
    public object DoAlgorithm(object data)
    {
        var list = data as List<string>;
        list.Sort();

        return list;
    }
}

class ConcreteStrategyB : IStrategy
{
    public object DoAlgorithm(object data)
    {
        var list = data as List<string>;
        list.Sort();
        list.Reverse();

        return list;
    }
}

//客户端代码
var context = new Context();

Console.WriteLine("Client: Strategy is set to normal sorting.");
context.SetStrategy(new ConcreteStrategyA());
context.DoSomeBusinessLogic();
            
Console.WriteLine();
            
Console.WriteLine("Client: Strategy is set to reverse sorting.");
context.SetStrategy(new ConcreteStrategyB());
context.DoSomeBusinessLogic();

/*运行结果
Client: Strategy is set to normal sorting.
Context: Sorting data using the strategy (not sure how it'll do it)
a,b,c,d,e

Client: Strategy is set to reverse sorting.
Context: Sorting data using the strategy (not sure how it'll do it)
e,d,c,b,a
*/
```

##### 适合策略模式的地方

- 当你想使用对象中各种不同的算法变体，并希望能在运行时切换算法时，可使用策略模式。
- 当你有许多仅在执行某些行为时略有不同的相似类时，可使用策略模式。
- 如果算法在上下文的逻辑中不是特别重要，使用该模式能将类的业务逻辑与其算法实现细节隔离开来。
- 当类中使用了复杂条件运算符以在同一算法的不同变体中切换时，可使用该模式。

##### 策略模式的优缺点

**优点** ：

- 你可以在运行时切换对象内的算法。
- 你可以将算法的实现和使用算法的代码隔离开来。
- 你可以使用组合来代替继承。
- 符合OCP

**缺点** ：

- 如果你的算法极少发生改变，那么没有任何理由引入新的类和接口。使用该模式只会让程序过于复杂。
- 客户端必须知晓策略间的不同——它需要选择合适的策略。
- 许多现代编程语言支持函数类型功能，允许你在一组匿名函数中实现不同版本的算法。这样，你使用这些函数的方式就和使用策略对象时完全相同，无需借助额外的类和接口来保持代码简洁。

#### Template Method(模板方法模式)

模板方法模式是一种行为设计模式，它在超类中定义了一个算法的框架，允许子类在不修改结构的情况下重写算法的特定步骤。

##### 问题

假如你正在开发一款分析公司文档的数据挖掘程序。 用户需要向程序输入各种格式 （PDF、 DOC 或 CSV） 的文档，程序则会试图从这些文件中抽取有意义的数据，并以统一的格式将其返回给用户。

该程序的首个版本仅支持 DOC 文件。在接下来的一个版本中，程序能够支持 CSV 文件。一个月后，你 “教会” 了程序从 PDF 文件中抽取数据。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220826213247.png)

一段时间后，你发现这三个类中包含许多相似代码。 尽管这些类处理不同数据格式的代码完全不同，但数据处理和分析的代码却几乎完全一样。如果能在保持算法结构完整的情况下去除重复代码，这难道不是一件很棒的事情吗？

还有另一个与使用这些类的客户端代码相关的问题：客户端代码中包含许多条件语句，以根据不同的处理对象类型选择合适的处理过程。如果所有处理数据的类都拥有相同的接口或基类，那么你就可以去除客户端代码中的条件语句，转而使用多态机制来在处理对象上调用函数。

##### 解决方案

模板方法模式建议将算法分解为一系列步骤，然后将这些步骤改写为方法，最后在 “模板方法” 中依次调用这些方法。步骤可以是抽象的，也可以有一些默认的实现。为了能够使用算法，客户端需要自行提供子类并实现所有的抽象步骤。如有必要还需重写一些步骤 （但这一步中不包括模板方法自身）。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220826213427.png)

首先， 我们将所有步骤声明为 抽象类型， 强制要求子类自行实现这些方法。 在我们的例子中， 子类中已有所有必要的实现， 因此我们只需调整这些方法的签名， 使之与超类的方法匹配即可。

现在，让我们看看如何去除重复代码。对于不同的数据格式，打开和关闭文件以及抽取和解析数据的代码都不同，因此无需修改这些方法。但分析原始数据和生成报告等其他步骤的实现方式非常相似，因此可将其提取到基类中，以让子类共享这些代码。

正如你所看到的那样，我们有两种类型的步骤：

- 抽象步骤必须由各个子类来实现
- 可选步骤已有一些默认实现，但仍可在需要时进行重写

还有另一种名为钩子的步骤。钩子是内容为空的可选步骤。即使不重写钩子，模板方法也能工作。钩子通常放置在算法重要步骤的前后，为子类提供额外的算法扩展点。

##### 模板方法模式结构

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220826214113.png)

1.**抽象类(Abstract­Class)** 会声明作为算法步骤的方法，以及依次调用它们的实际模板方法。算法步骤可以被声明为 抽象类型，也可以提供一些默认实现。

2.**具体类(Con­crete­Class)** 可以重写所有步骤，但不能重写模板方法自身。

##### 伪代码

本例中的模板方法模式为一款简单策略游戏中人工智能的不同分支提供 “框架”。游戏中所有的种族都有几乎同类的单位和建筑。因此你可以在不同的种族上复用相同的 AI 结构，同时还需要具备重写一些细节的能力。通过这种方式，你可以重写半兽人的 AI 使其更富攻击性，也可以让人类侧重防守，还可以禁止怪物建造建筑。在游戏中新增种族需要创建新的 AI 子类，还需要重写 AI 基类中所声明的默认方法。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220826214223.png)

```csharp
//这下真的是伪代码了
// 抽象类定义了一个模板方法，其中通常会包含某个由抽象原语操作调用组成的算
// 法框架。具体子类会实现这些操作，但是不会对模板方法做出修改。
abstract class GameAI
{
    //某些步骤可以在基类中实现
    public void turn()
    {
        collectResources();
        buildStructures();
        buildUnits();
        attack();
    }

    public void collectResources()
    {
        foreach(var s in this.builtStructures)
        {
            s.collect();
        }
    }

    public abstract void buildStructures();
    public abstract void buildUnits();

    public void attack()
    {
        var enemy = cloestEnemy();
        if(enemy == null)
        {
            sendScouts(map.center);
        }
        else 
            sendWarriors(enemy.position);
    }

    public abstract void sendScouts(position);
    public abstract void sendWarriors(position);
}

class OrcsAI : GameAI
{
    public override void buildStructures()
    {
        if (there are some resources) 
        {
            // 建造农场，接着是谷仓，然后是要塞。
        }
    }

    public override void buildUnits()
    {
        if (there are plenty of resources) 
        {
            if (there are no scouts)
            {
                // 建造苦工，将其加入侦查编组。
            }
            else
            {
                // 建造兽族步兵，将其加入战士编组。
            }
        }
    }

    public override void sendScouts(position)
    {
        if(scouts.length > 0)
        {
            // 将侦查编组送到指定位置。
        }
    }

    public override void sendWarriors(position)
    {
        if(warriors.length > 5)
        {
            // 将战斗编组送到指定位置。
        }
    }
}

class MonstersAI : GameAI
{
    public override void collectResources()
    {
        // 怪物不会采集资源。
    }

    public override void buildStructures()
    {
        // 怪物不会建造建筑。
    }

    public override void buildUnits()
    {
        // 怪物不会建造单位。
    }
}
```

##### 适合模板方法模式的地方

- 当你只希望客户端扩展某个特定算法步骤，而不是整个算法或其结构时，可使用模板方法模式。
- 当多个类的算法除一些细微不同之外几乎完全一样时，你可使用该模式。但其后果就是，只要算法发生变化，你就可能需要修改所有的类。

##### 模板方法的优缺点

**优点** ：

- 你可仅允许客户端重写一个大型算法中的特定部分，使得算法其他部分修改对其所造成的影响减小。
- 你可将重复代码提取到一个超类中。

**缺点** ：

- 部分客户端可能会受到算法框架的限制。
- 通过子类抑制默认步骤实现可能会导致违反里氏替换原则(Liskov)。
- 模板方法中的步骤越多， 其维护工作就可能会越困难。

#### Visitor(访问者模式)

访问者模式是一种行为设计模式，它能将算法与其所作用的对象隔离开来。

##### 问题

假如你的团队开发了一款能够使用巨型图像中地理信息的应用程序。图像中的每个节点既能代表复杂实体 （例如一座城市），也能代表更精细的对象 （例如工业区和旅游景点等）。如果节点代表的真实对象之间存在公路，那么这些节点就会相互连接。在程序内部，每个节点的类型都由其所属的类来表示，每个特定的节点则是一个对象。

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220826224114.png)

一段时间后，你接到了实现将图像导出到 XML 文件中的任务。这些工作最初看上去非常简单。你计划为每个节点类添加导出函数，然后递归执行图像中每个节点的导出函数。解决方案简单且优雅：使用多态机制可以让导出方法的调用代码不会和具体的节点类相耦合。

但你不太走运，系统架构师拒绝批准对已有节点类进行修改。他认为这些代码已经是产品了，不想冒险对其进行修改，因为修改可能会引入潜在的缺陷。

此外，他还质疑在节点类中包含导出 XML 文件的代码是否有意义。这些类的主要工作是处理地理数据。导出 XML 文件的代码放在这里并不合适。

还有另一个原因，那就是在此项任务完成后，营销部门很有可能会要求程序提供导出其他类型文件的功能，或者提出其他奇怪的要求。这样你很可能会被迫再次修改这些重要但脆弱的类。

##### 解决方案

访问者模式建议将**新行为放入一个名为访问者的独立类中，而不是试图将其整合到已有类中**。现在，需要执行操作的原始对象将作为参数被传递给访问者中的方法，让方法能访问对象所包含的一切必要数据。

##### 访问者模式结构

![img](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/DesignPatternsRuMen/20220826230156.png)

1.**访问者(Vis­i­tor)** 接口声明了一系列以对象结构的具体元素为参数的访问者方法。如果编程语言支持重载，这些方法的名称可以是相同的，但是其参数一定是不同的。

2.**具体访问者(Con­crete Vis­i­tor)** 会为不同的具体元素类实现相同行为的几个不同版本。

3.**元素(Ele­ment)** 接口声明了一个方法来 “接收” 访问者。该方法必须有一个参数被声明为访问者接口类型。

4.**具体元素(Con­crete Ele­ment)** 必须实现接收方法。该方法的目的是根据当前元素类将其调用重定向到相应访问者的方法。请注意，即使元素基类实现了该方法，所有子类都必须对其进行重写并调用访问者对象中的合适方法。

5.**客户端(Client)** 通常会作为集合或其他复杂对象（例如一个组合树）的代表。客户端通常不知晓所有的具体元素类，因为它们会通过抽象接口与集合中的对象进行交互。

##### 伪代码

访问者不是常用的设计模式，因为它不仅复杂，应用范围也比较狭窄。

```csharp
//Component接口声明一个accept方法来使用visitor接口
public interface IComponent
{
    void Accept(IVisitor visitor);
}
//具体Component类
public class ConcreteComponentA : IComponent
{
    public void Accept(IVisitor visitor)
    {
        visitor.VisitCOncreteComponentA(this);
    }

    //具体Component类中一些自己的方法
    public string ExclusiveMethodOfConcreteComponentA()
    {
        return "A";
    }
}
public class ConcreteComponentB : IComponent
{
    public void Accept(IVisitor visitor)
    {
        visitor.VisitCOncreteComponentB(this);
    }

    //具体Component类中一些自己的方法
    public string ExclusiveMethodOfConcreteComponentB()
    {
        return "B";
    }
}
//Visitor接口声明一系列访问Component的方法
public interface IVisitor
{
    void VisitConcreteComponentA(ConcreteComponentA element);

    void VisitConcreteComponentB(ConcreteComponentB element);
}
class ConcreteVisitor1 : IVisitor
{
    public void VisitConcreteComponentA(ConcreteComponentA element)
    {
        Console.WriteLine(element.ExclusiveMethodOfConcreteComponentA() + " + ConcreteVisitor1");
    }

    public void VisitConcreteComponentB(ConcreteComponentB element)
    {
        Console.WriteLine(element.SpecialMethodOfConcreteComponentB() + " + ConcreteVisitor1");
    }
}
class ConcreteVisitor2 : IVisitor
{
    public void VisitConcreteComponentA(ConcreteComponentA element)
    {
        Console.WriteLine(element.ExclusiveMethodOfConcreteComponentA() + " + ConcreteVisitor2");
    }

    public void VisitConcreteComponentB(ConcreteComponentB element)
    {
        Console.WriteLine(element.SpecialMethodOfConcreteComponentB() + " + ConcreteVisitor2");
    }
}
public class Client
{
    public static void ClientCode(List<IComponent> components, IVisitor visitor)
    {
        foreach (var component in components)
        {
            component.Accept(visitor);
        }
    }
}
//客户端代码
List<IComponent> components = new List<IComponent>
{
    new ConcreteComponentA(),
    new ConcreteComponentB()
};

Console.WriteLine("The client code works with all visitors via the base Visitor interface:");
var visitor1 = new ConcreteVisitor1();
Client.ClientCode(components,visitor1);

Console.WriteLine();

Console.WriteLine("It allows the same client code to work with different types of visitors:");
var visitor2 = new ConcreteVisitor2();
Client.ClientCode(components, visitor2);
/*运行结果
The client code works with all visitors via the base Visitor interface:
A + ConcreteVisitor1
B + ConcreteVisitor1

It allows the same client code to work with different types of visitors:
A + ConcreteVisitor2
B + ConcreteVisitor2
*/
```

##### 适合访问者模式的地方

- 如果你需要对一个复杂对象结构（例如对象树）中的所有元素执行某些操作，可使用访问者模式。
- 可使用访问者模式来清理辅助行为的业务逻辑。
- 当某个行为仅在类层次结构中的一些类中有意义， 而在其他类中没有意义时，可使用该模式。

##### 访问者模式的优缺点

**优点** ：

- 符合OCP
- 符合SRP
- 访问者对象可以在与各种对象交互时收集一些有用的信息。当你想要遍历一些复杂的对象结构（例如对象树），并在结构中的每个对象上应用访问者时，这些信息可能会有所帮助。

**缺点** ：

- 每次在元素层次结构中添加或移除一个类时，你都要更新所有的访问者。
- 在访问者同某个元素进行交互时， 它们可能没有访问元素私有成员变量和方法的必要权限。

### 后记

这次花了差不多20天的时间来写这一个博客记录一下关于设计模式的学习，其实看书的时间不算长，主要花时间的是写出让人容易懂的博客。学习了初步的设计模式的知识，以前看过的但是不是很懂的知识突然就明白了一些。当然，由于自身还没写过上万行的代码，后面肯定还会在复习一下设计模式，不过看的书应该是讲解地更深入的书籍。

### 参考文献

- 《敏捷软件设计开发》
- https://refactoring.guru/design-patterns(通俗易懂地讲解设计模式的网站，大部分例子是引用它的)
- https://www.runoob.com/design-pattern/design-pattern-tutorial.html(菜鸟教程中的设计模式，提供更多的例子来学习)