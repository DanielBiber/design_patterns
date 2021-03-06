# Patterns Introduction（设计模式介绍）

## Strategy Pattern（策略模式）
策略模式定义了算法族，分别封装起来，让他们之间可以互相替换，此模式让算法的变化独立于使用算法的客户。

### 应用场景
1. 多个类只区别在表现行为不同，可以使用Strategy模式，在运行时动态选择具体要执行的行为。
2. 需要在不同情况下使用不同的策略(算法)，或者策略还可能在未来用其它方式来实现。
3. 对客户隐藏具体策略(算法)的实现细节，彼此完全独立。

## Observer Pattern（观察者模式）
观察者模式定义了对象之间的一对多依赖，这样一来，当一个对象改变状态时，他的所有依赖者都会收到通知并自动更新。
观察者模式提供了一种对象设计，让主题和观察者之间松耦合

## Decorator Pattern（装饰者模式）
装饰者模式动态地将责任附加到对象上。若要扩展功能，装饰者提供了比继承更有弹性的替代方案。
装饰者模式主要有Component、ConcreteComponent、Decorator和ConcreteDecorator组成：
1. 抽象组件角色(Component)：定义一个对象接口，以规范准备接受附加责任的对象，即可以给这些对象动态地添加职责。
2. 具体组件角色(ConcreteComponent) :被装饰者，定义一个将要被装饰增加功能的类。可以给这个类的对象添加一些职责。
3. 抽象装饰者(Decorator):维持一个指向构件Component对象的实例，并定义一个与抽象组件角色Component接口一致的接口。
4. 具体装饰者角色（ConcreteDecorator):向组件添加职责。

python 装饰器可以更简单实现装饰者模式

## Factory Pattern（工厂模式）
### 工厂方法模式
工厂方法用来处理对象的创建，并将这样的行为封装在子类中。这样，客户程序中关于超类的代码就和子类对象创建代码解耦了。

工厂模式用来封装对象的创建。工厂方法模式通过让子类决定该创建的对象是什么，来达到将对象创建的过程封装的目的。

工厂方法模式定义了一个对象创建接口，但是由子类决定要实例化的类是哪一个，工厂方法让类把实例化推迟到子类。

工厂方法模式通常包括创建者（Creator，具体的创建者实现工厂方法）和 产品（Product）。
创建者类是抽象创建者类，它定义了一个抽象的工厂方法，让子类实现此方法制造产品。
创建者通常包含依赖于抽象产品的代码，而这些抽象产品由子类制造，创建者不需要真的知道在制造那种具体产品。

工厂方法让子类决定要实例化那个类，并不是指允许子类在运行时决定，而是指在编写创建者类的时候，不需要知道实际创建的产品是哪个。选择使用了哪个子类，自然就决定了实际创建的产品是什么。

### Abstract Factory Pattern (抽象工厂模式)
抽象工厂模式提供一个接口，用于创建相关或依赖对象的家族，而不需要明确指定具体类。

抽象工厂允许客户使用抽象的接口来创建一组相关的产品，而不需要知道实际产出的具体产品是什么，这样客户从具体的产品解耦。

抽象工厂定义了一个接口，所有的具体工厂都必须实现此接口，这个接口包含一组方法用来生产产品。

### 比较
- 工厂方法使用继承：把对象的创建委托给子类，子类实现工厂方法来创建对象。可以把客户代码从需要实例化的具体类中解耦，或者如果还不知道将来需要实例化哪些具体类时，也可以使用工厂方法。
工厂方法使用简单，只需要继承成子类，并实现工厂方法即可。
- 抽象工厂使用组合：提供一个用来创建产品家族的抽象类型，类型的子类定义了产品被产生的方法，要使用这个工厂必须先实例化它，
然后将它传入一些针对抽象类型所写的代码中。对象的创建被实现在工厂接口所暴露出来的方法中。当需要创建产品家族和想让制造的相关产品集合起来时，可以使用抽象工厂。

## Singleton Pattern（单例模式）
单例模式确保一个类只有一个实例，并提供一个全局访问点。

## Command Pattern （命令模式）
命令模式将「请求」封装成对象，以便使用不同的请求、队列或者日志来参数化其他对象。命令模式也支持可撤销的操作。

命令模式将一个请求封装为一个对象，从而使我们可用不同的请求对客户进行参数化；对请求排队或者记录请求日志，以及支持可撤销的操作。
命令模式是一种对象行为型模式，其别名为动作(Action)模式或事务(Transaction)模式。
- 一个命令对象通过在特定接收者上绑定一组动作来封装一个请求，命令对象将动作和接受者包进对象中，暴露出一个 `execute()` 方法
- 一个命令对象需要有相应的接受者，`execute()`方法调用接受者的一个或多个动作
- 调用者持有命令对象，在特定时间执行命令对象的`execute()`方法

### 命令模式的其他应用
- 队列请求：一端添加命令，另一端取出命令，执行命令的 `execute()` 方法，这样工作队列类和进行计算的对象之间完全解耦
- 日志请求：将执行动作记录在日志中，在系统死机重启后调用这些动作恢复到之前的状态。命令模式通过新增方法 `load()` 和 `store()` 可以支持。需要将对象序列化并持久化到日志中。

## Adapter Pattern （适配器模式）
客户使用适配器模式的过程如下：
- 客户通过目标接口调用适配器的方法对适配器发出请求
- 适配器使用被适配者接口把请求转换成被适配者的一个或多个调用接口
- 客户接受到调用的结果，但并未察觉这一切是适配器在起转换作用
适配器模式是将一个类的接口，转换成客户期望的另一个接口，适配器让原本接口不兼容的类可以合作无间。
适配器有良好的 OO 设计原则: 使用对象组合，以修改的接口包装被适配者，被适配者的任何子类都可以搭配着适配器使用。

对象适配器和类适配器使用两种不同的适配方法：分别是组合与集成。对象适配器使用组合，类适配器使用多重继承。
适配器并不完美，客户必须小心潜在的异常。

## Facade Pattern （外观模式）
外观模式将一个或数个类的复杂的一切隐藏在背后，只露出简化的接口。
外观模式不只是简化了接口，也将客户从组件的子系统中解耦。

外观模式提供了一个统一的接口，用来访问子系统中的一群接口。外观定义了一个高层接口，让子系统更容易使用。

### 外观 VS 适配器 vs 装饰者
外观和适配器都可以包装许多类。但是外观的意图是简化接口。而适配器的意图是将接口转换成不同接口。
装饰者将一个对象包装起来以增加新的行为和责任，不改变接口。

## Template Method Pattern（模板方法模式）
模板方法定义了一个算法的步骤，并允许子类为一个或多个步骤提供实现

模板方法模式在一个方法中定义一个算法的骨架，而将一些步骤延迟到子类中。模板方法使得子类可以
在不改变算法结构的情况下，重新定义算法中的某些步骤。

模板方法将算法定义成一组步骤，其中的任何步骤都可以是抽象的，由子类负责实现。这样可以确保
算法的结构保持不变，同时由子类提供部分实现。

### 对模板方法挂钩
钩子（Hook）是一种被声明在抽象类中的方法，但是只有空的或者默认的实现。钩子的存在可以让子类
有能力对算法的不同点进行挂钩，要不要挂钩由子类自行决定。

当子类必须提供算法中的某个方法或步骤的实现时，可以使用抽象方法。如果算法的这个部分是可选的，
使用钩子。如果是钩子的话，子类可以选择实现这个钩子，但并不强制这么做。

钩子可以让子类实现算法中可选部分；钩子让子类能够有机会对模板方法中某些即将发生（或刚刚发生）的步骤作出反应。

### 模板方法模式 VS 策略模式
- 模板方法定义了算法的步骤，子类定义某些步骤的内容；策略模式通过对象组合的方式，让客户选择算法的实现
- 模板方法在超类中提供了基础的方法，达到代码复用，并允许子类指定行为；策略模式通过对象组合，使得客户可以在运行时改变他们的算法，改用不同的策略对象
- 模板方法使用集成；策略模式使用组合
- 工厂方法是模板方法的一种特殊版本

## Iterator Pattern （迭代器模式）
迭代器模式提供一种方法顺序访问一个聚合对象中的各个元素，而不是暴露其内部的表示。

把游走的任务放在迭代器上，而不是聚合上，这样简化了聚合的接口和实现，也让责任各得其所。

## Composite Pattern （组合模式）
组合模式允许你将对象组合成树形结构来表现 “整体/部分” 层次结构。

组合能让客户以一致的方式处理个别对象以及对象组合。

组合模式让我们能用树形方式创建对象的结构，树里面包含了组合以及个别的对象。

使用组合结构，我们能把相同的操作应用在组合和个别对象上。在大多数情况下，我们可以忽略对象组合和个别对象之间的差别。

组合模式提供了一个结构，可以同时包容个别对象和组合对象。

组合模式允许客户对个别对象以及组合对象一视同仁。

组合结构内的任意对象称为组件，组件可以是组合也可以是叶节点。

在实现组合模式时，有许多设计上的折中。要根据需要平衡透明性和安全性。

## State Pattern （状态模式）
状态模式允许对象在内部状态改变时改变它的行为，对象看起来好像修改了它的类。

状态模式将状态封装成独立的类，并将动作委托到代表当前状态的对象，行为会随着内部状态而改变。

当状态转换是固定的时候，适合放在 Context 中；当转换是更动态的时候，放在状态类中。

将状态转换放在状态类中的缺点是：状态直接产生了依赖。

状态用在 Context 中来代表它的内部状态及行为的，所以只有 Context 才会对状态提出请求。
客户不会直接改变 Context 的状态，不会直接和状态交互。

状态转换可以由 State 类或 Context 类控制

状态模式通常会导致设计中类的数目大量增加。

状态类可以被多个 Context 实例共享

### 策略模式 VS 状态模式
- 策略模式通常会用行为或算法来配置 Context 类
- 状态模式允许 Context 随着状态的改变而改变行为

## Proxy Pattern （代理模式）

### 远程代理
客户对象所做的就像是在做远程方法调用，但其实只是调用本地堆中的“代理”对象上的方法，
再由代理处理所有网络通信的低层细节。

**客户端：**
客户调用客户辅助对象的方法，以为客户辅助对象就是真正的服务。

客户辅助对象负责转发客户请求，传送方法调用信息，等待服务器的返回。

**服务器端**

服务辅助对象从客户辅助对象接收请求（通过网络 socket），将调用信息捷豹，然后调用真正的服务器对象上的真正方法。
服务辅助对象从服务中得到返回值，将返回值打包，然后返回到客户辅助对象（通过网络 socket），
客户辅助对象对信息解包，最后将返回值交给客户对象。

RMI 将客户辅助对象称为 stub（桩），服务辅助对象称为 skeleton（骨架）

### 代理模式
代理模式为另一个对象提供一个替身或者占位符以控制对这个对象的访问。

使用代理模式创建代表（representative）对象，让代表对象控制某对象的访问，被代理的对象可以是
远程的对象、创建开销大的对象或需要安全控制的对象。

代理控制访问的方式：
- 远程代理控制访问远程对象
- 虚拟代理控制访问创建开销大的资源
- 保护代理基于权限控制对资源的访问

### Subject
为 RealSubject 和 Proxy 提供接口。通过实现同一接口，Proxy 在 RealSubject 出现的地方取代它。

### RealSubject
RealSubject 是真正做事的对象，是被 Proxy 代理和控制访问的对象

### Proxy
Proxy 持有 RealSubject 的引用。客户和 RealSubject 的交互都必须通过 Proxy。
因为 Proxy 和 RealSubject 实现相同的接口（Subject），所以任何用到 RealSubject 的地方，都可以
用 Proxy 取代。Proxy 也控制了对 RealSubject 的访问，如：RealSubject 是远程对象，RealSubject 创建开销大，
RealSubject 需要被保护。

### 虚拟代理
虚拟代理作为创建开销大的对象的代表。虚拟代理经常到我们真正需要一个对象的时候才创建它。
当对象在创建前和创建中时，由虚拟代理来扮演对象的替身。对象创建后，代理将请求直接委托给对象。

### 防火墙代理
控制网络资源的访问，保护主题免于“坏客户”的侵害

### 智能引用代理
当主题被引用时，进行额外的动作，例如计算一个对象被引用的次数

### 缓存代理
为开销大的运算结果提供暂时的存储：它也允许多个客户共享结果，以减少计算或网络延迟

### 同步代理
同步代理在多线程的情况下为主题提供安全的访问

### 复杂隐藏代理
用来隐藏一个类的复杂集合的复杂度，并进行访问控制。有时候也称为外观代理。复杂隐藏代理和外观
模式是不一样的，因为代理控制访问，而外观模式值提供另一组接口。

### 写入时复制代理
用来控制对象的复制，方法是延迟对象的复制，直到客户真的需要为止。这是虚拟代理的辩题。


## 复合模式（Compound Pattern）
模式通常被遗弃使用，并被组合在同一个设计解决方案中。

复合模式在一个解决方案中结合两个或多个模式，以解决一般或重复发生的问题。

### MVC（模型-视图-控制器）
#### 视图
用来呈现模型。视图通常直接从模型中取得它需要显示的状态与数据。

#### 控制器
取得用户的输入并解读其对模型的意思。

控制器不会实现应用逻辑，控制器为视图实现行为。它聪明地将视图的动作转换成模型上的动作。
模型实现应用逻辑，并决定如何响应动作。控制器需要决定调用哪个模型的哪个方法，不是应用逻辑。
应用逻辑指的是管理与操作你的模型中的数据的代码。

#### 模型
模型持有所有的数据，状态和程序逻辑。模型没有注意到视图和控制台，虽然它提供了操作和检索状态
的接口，并发送状态改变通知给观察者。

在 MVC 中，模型对视图和控制器一无所知，它们之间是解耦的。模型只知道一些观察者它需要通知。

#### MVC 包含的模式
- 视图和控制器实现了**策略模式**
- 模型实现了**观察者模式**
- 视图实现了**组合模式**

## 桥接模式（Bridge Pattern）
桥接模式通过将实现和抽象放在两个不同的类层次中而使他们可以独立改变。

### 桥接的优点
- 将实现予以解耦，让它和界面之间不再永久绑定
- 抽象和实现可以独立扩展，不会影响到对方
- 对于“具体的抽象类”所做的改变不会影响到客户

### 桥接的用途和缺点
- 桥接适合使用在需要跨越多个平台的图形和窗口系统上
- 当需要用不同的方式改变接口和实现时，适合使用桥接模式
- 桥接模式的缺点是增加了复杂度

## 生成器模式（Builder Pattern）
生成器模式封装一个产品的构造过程，并允许按步骤构造

### 生成器的优点
- 将一个复杂对象的创建过程封装起来
- 允许对象通过多个步骤来创建，并且可以改变过程（这和只有一个步骤的工厂模式不同）
- 向客户隐藏产品内部实现
- 产品的实现可以被替换，因为客户只看到一个抽象的接口

### 生成器的用途和缺点
- 经常被用来创建组合结构
- 与工厂模式相比，采用生成器模式创建对象的客户，需要具备更多的领域知识

## 责任链（Chain of Responsibility Pattern）
当你想要让一个以上的对象有机会能够处理某个请求的时候，就使用责任链模式

通过责任链模式，你可以为某个请求创建一个对象链。每个对象依序检查次请求，并对其进行处理，或者
将它传给链中的下一个对象。

链中的每个对象扮演处理器，并且有一个后继对象。如果它可以处理请求，就进行处理，否则就把请求
发给后继者。

### 责任链的优点
- 将请求的发送者和接受者解耦
- 可以简化你的对象，因为它不需要知道链的结构
- 通过改变链内的成员或调动它们的次序，允许你动态地新增或删除责任

### 责任链的用途和缺点
- 经常被使用在窗口系统中，处理鼠标和键盘之类的事件
- 并不保证请求一定会被执行；如果没有任何对象处理它的话，它可能会落到链尾端之外
- 可能不容易观察运行时的特征，有碍于除错

## 蝇量模式（Flyweight Pattern）
如果想让某个类的一个实例能用来提供许多“虚拟实例”，就使用蝇量模式

### 蝇量的优点
- 减少运行时对象实例的个数，节省内存
- 将许多“虚拟”对象的状态集中管理

### 蝇量的用途和缺点
- 当一个类有许多的实例，而这些实例能被同一个方法控制的时候，就可以使用蝇量模式
- 蝇量模式的缺点在于，一旦你实现了它，那么单个的逻辑实例将无法拥有独立而不同的行为

## 解释器模式（Interpreter Pattern）
解释权模式为语言创建解释权

### 解释器模式的优点
- 将每一个语法规则表示成一个类，方便于实现语言
- 因为语法由许多类标识，所以可以轻易地改变或扩展此语言
- 通过在类结构中加入新的方法，可以在解释的同时增加新的行为，例如打印格式的美化或者进行复杂的程序验证

### 解释器的用途和缺点
- 当你需要实现一个简单的语言时，使用解释器
- 当你有一个简单的语法，而且简单比效率更重要时，使用解释器
- 可以处理脚本语言和编程语言
- 当语法规则的数据太大时，这个模式可能会变得非常繁杂。这种情况下，使用解释权/编译器的产生器可能更合适。

## 中介者模式（Mediator Pattern）
使用中介者模式来集中相关对象之间复杂的沟通和控制方式

- 每个对象都会在自己状态改变时，告诉中介者
- 每个对象都会对中介者所发出的请求作出回应

有了中介者之后，对象之间彻底解耦

中介者内包含了整个系统的控制逻辑。当某个装置需要一个新的规则时，或者一个新的装置被加入系统内，
其所有需要用到的逻辑也都被加进了中介者内。

### 中介者的优点
- 通过将对象彼此解耦，可以增加对象的复用性
- 通过将控制逻辑集中，可以简化系统维护
- 可以让对象之间所传递的消息变得简单而且大幅减少

### 中介者的用途和缺点
- 中介者常被用来协调相关的 GUI 组件
- 中介者模式的缺点是，如果设计不当，中介者对象本身会变得过于复杂

## 备忘录模式（Memento Pattern）
当你需要让对象返回之前的状态时，就使用备忘录模式

备忘录模式有两个目标：
- 存储系统关键对象的重要状态
- 维护关键对象的封装

### 备忘录的有点
- 将被存储的状态放在外面，不要和关键对象混在一起，这可以维护内聚
- 保持关键对象的数据封装
- 提供容易实现的恢复能力

### 备忘录的用途和缺点
- 备忘录用于存储状态
- 使用备忘录的缺点：存储和恢复状态的过程可能相当耗时
- 在 Java 系统中，其实可以考虑使用序列化机制存储系统的状态

## 原型模式（Prototype Pattern）
当创建给定类的实例的过程很昂贵或很复杂时，就使用原型模式

原型模式允许你通过复制现有的实例来创建新的实例。客户的代码在不知道要实例化何种特定种类的情况下，
可以制造出新的实例。

### 原型的优点
- 向客户隐藏制造新实例的复杂性
- 提供让客户能够产生未知类型对象的选项
- 在某些环境下，复制对象比创建对象更有效

### 原型的用途和缺点
- 在一个复杂的类层次中，当系统必须从其中的许多类型创建新对象时，可以考虑原型
- 使用原型模式的缺点：对象的复制有时相当复杂

## 访问者模式（Visitor Pattern）
当你想要为一个对象的组合增加新的能力，且封装并不重要时，就使用访问者模式

访问者必须参观组合内的每个元素，这样的功能是在导游对象中，访问者通过导游的引导，收集组合中所有对象
的状态，一旦状态被收集了，客户就可以让访问者对状态进行各种操作。当需要新的功能时，只要加强访问者即可。

客户要求访问者从组合结构中取得信息，新方法可以被加入到访问者中，而不影响组合

访问者需要能够调用每个类的 getState()，而这也正是你能够加入新方法让客户使用的地方

所有这些组合类必须做的事情，就是加入一个 getState() 方法（而不必担心暴露他们自己）


### 访问者的优点
- 允许你对组合结构加入新的操作，而无需改变结构本身
- 想要加入新的操作，相对容易
- 访问者所进行的操作，其代码是集中在一起的

### 访问者的用途和缺点
- 当采用访问者模式的时候，就会打破组合类的封装
- 因为游走的功能牵涉其中，所以对组合结构的改变就会更加困难
