# HeadFirstDesignPatternsCode
实现《Head First Design Patterns》一书中的代码，并整理相关的个人笔记。

[原书作者的GitHub代码地址](https://github.com/bethrobson/Head-First-Design-Patterns)

## 第0章 全书中每一章节的小结

### (1) OO原则

> * 封装变化；
> * 多用组合，少用继承；
> * 针对接口编程，不针对实现编程；
> * 为交互对象之间的松耦合设计而努力；
> * 对扩展开放，对修改关闭；

---

## 第1章 设计模式入门--欢迎来到设计模式的世界

### (1)一个概念

&emsp;&emsp;在软件开发过程中，一个伴随我们不变的真理：change。不轮当初软件设计的多好，一段时间后，总是需要成长与改变。否则软件就会“死亡”。

### (2)设计原则1

&emsp;&emsp;**找出应用中可能需要变化之处，把他们独立出来，不要和那些不需要变化的代码混在一起**。

&emsp;&emsp;这样的概念很简单，几乎是每个设计模式背后的精神所在。**所有的设计模式都提供了一套方法让“系统中的某部分改变不会影响其他部分”。**

### (3)设计原则2

&emsp;&emsp;**针对接口编程，而不是针对实现编程**。

### (4)设计原则3

&emsp;&emsp;**多用组合，少用继承**。

&emsp;&emsp;使用组合建立系统具有很大的弹性，不仅可以将算法族封装成类，更可以在“**运行时动态的改变行为**”，只要组合的行为对象符合正确的接口标准即可以。

### (5)策略模式的定义

&emsp;&emsp;**策略模式定义了算法族，分别封装起来，让他们之间可以互相替换，此模式让算法的变化独立于使用算法的客户**。

### (6)本章的一点补充

> * (1) 大多数的模式和原则，都着眼于软件变化的主题；
> * (2）大多数的模式都**允许系统局部改变独立于其他部分**；

---

## 第2章 观察者模式--让你的对象知悉现状

### (1) 定义

&emsp;&emsp;观察者模式：**定义对象间的一对多的依赖关系，当一个对象改变状态时，它的所有依赖者都会收到通知并自动更新。**

&emsp;&emsp;主题(Subject)是真正拥有数据的人，观察者是多个主题的依赖者，在数据发生变化时更新，这样比起让许多对象控制同一份数据来，可以的得到更干净的OO设计。

&emsp;&emsp;设计原则：为了交互对象之间的松耦合设计而努力。松耦合的设计之所以能让我们建立有弹性的OO系统，能够应对变化，**是因为对象之间的互相依赖降到了最低**。

### (2) java内置的观察者模式的不足

> * (1)可观察类Observble是一个“类”而不是一个“接口”，更糟糕的是，它甚至没有实现一个接口。这极大的限制了他的复用和使用；
> * (2)Observble将关键的方法保护起来，比如setChanged()，他被定义成protected。这意味着，**除非你继承自Observable，否则你无法创建Observable实例并组合到自己的对象中来，**这个违反了第二个设计原则，**多用组合，少用继承**。

### (3) 挑战设计原则

#### a.设计原则：找出程序中会变化的方面，然后将其和固定不变的方面相分离。

&emsp;&emsp;在观察者模式中，会改变的是主题的状态，以及观察者的数目和类型，用这个模式，你可以依赖于主题状态的对象，都不必改变主题，这就叫提前规划。

#### b.设计原则：针对接口编程，不针对实现编程

&emsp;&emsp;主题与观察者都是用接口，观察者利用主题的接口向主题注册，而主题利用观察者接口通知观察者，这样可以让他们之间运作正常，又同时具有松耦合的优点。

#### c.设计原则：多用组合，少用继承

&emsp;&emsp;**观察者模式利用“组合”将许多观察者组合进主题中，对象之间的这种关系不是通过继承产生的，而是在运行时利用组合的方式而产生的。**

---

## 第3章 装饰者模式--装饰对象

&emsp;&emsp;本章可以称为**给爱用继承的人一个全新的设计眼界**。通过使用对象组合的方式，做到运行时装饰类。

### (1)设计原则

**类应该对扩展开放，对修改关闭。**

### (2) 关于装饰者模式的一些概念

> * (1) **装饰者和被装饰者有相同的超类型；**
> * (2) 你可以用一个或多个装饰者包装同一个对象；
> * (3) 由于装饰者和被装饰者拥有相同的父类，所以可以遵循里斯替换原则，在任何需要原始对象的场合，都可以使用装饰过的对象替代他。
> * (4) **装饰者可以在委托被装饰者的行为之前或者之后，加上自己的行为，以达到特定的目的；**
> * (5) 对象可以在任何时候被装饰，所以可以在运行时动态地，不限量地用你喜欢的装饰者来装饰对象；

### (3) 定义装饰者模式

&emsp;&emsp;**装饰者模式动态的将责任附加到对象上，若要扩展功能，装饰者提供了比继承更有弹性的替代方案。**

### (4) 以一个奶茶店的运营为例子来看

![装饰者模式类图类图](http://occl9k36n.bkt.clouddn.com/2017_03_25_decorate_pattern.png)

最终的测试代码：

``` java
public class DrinkStore {

	public static void main(String[] args) {
		Drinks drink = new GreenTea();
		System.out.println(drink.getDescription() + ":价格$" + drink.cost());
		
		Drinks drink2 = new Caffe();
		drink2 = new BingTang(drink2);
		drink2 = new NaiXi(drink2);
		System.out.println(drink2.getDescription() + ":价格$" + drink2.cost());
		
		Drinks drink3 = new RedTea();
		drink3 = new NingMeng(drink3);
		System.out.println(drink3.getDescription() + ":价格$" + drink3.cost());
	}

}

```

运行结果：

``` java
绿茶:价格$1.05
咖啡+冰糖+奶昔:价格$2.3400000000000003
红茶+柠檬:价格$0.99

```

关于装饰者模式的一些tips：

> * 继承属于扩展形式之一，但不见得是达到弹性设计的最佳方式；
> * 在我们的设计中，应该允许行为可以被扩展，而无需修改现有代码；
> * **组合和委托可用以在运行时动态的加上新的行为**；
> * 除了继承，装饰者模式也可以让我们扩展行为；
> * **装饰者模式意味着一群装饰者类**，这些类用来包装具体组件；
> * 装饰者会导致程序设计中出现许多小对象，如果过度使用，会让程序变得很复杂；

## 第4章 工厂模式--烘烤OO的精华

### (1)简单工厂

原书中的关于简单工厂的使用：

``` java
public class SimplePizzaFactory {

	public Pizza createPizza(String type) {
		Pizza pizza = null;

		if (type.equals("cheese")) {
			pizza = new CheesePizza();
		} else if (type.equals("pepperoni")) {
			pizza = new PepperoniPizza();
		} else if (type.equals("clam")) {
			pizza = new ClamPizza();
		} else if (type.equals("veggie")) {
			pizza = new VeggiePizza();
		}
		return pizza;
	}
}
```

&emsp;&emsp;**简单工厂其实不是一个设计模式**，反而比较像是一种编程习惯，但由于经常被使用，有些开发人员的确会把这个编程习惯误认为是“工厂模式”。

### (2)工厂方法

&emsp;&emsp;**现在实例化披萨的操作交给一个具体的方法去执行，此方法就如同是一个工厂。**

改进后的代码：
``` java
public abstract class PizzaStore {

	/**
	 * 现在实例化披萨的操作交给一个具体的方法去执行，
	 * 此方法就如同是一个工厂
	 * @param item
	 * @return
	 */
	abstract Pizza createPizza(String item);
	
	public Pizza orderPizza(String type) {
		Pizza pizza = createPizza(type);
		System.out.println("--- Making a " + pizza.getName() + " ---");
		pizza.prepare();
		pizza.bake();
		pizza.cut();
		pizza.box();
		return pizza;
	}
}
```


**工厂方法用来处理对象的创建，并将这样的行为封装在子类中。这样，客户端程序中关于超类的代码就和子类的对象创建代码解耦了。**

``` java
abstract Pizza createPizza(String item);
```

&emsp;&emsp;工厂方法模式**通过让子类决定该创建的对象是什么，来达到将对象创建的过程封装的目的**。

定义：

&emsp;&emsp;**工厂方法模式定义了一个创建对象的接口，但由子类决定要实例化的类是哪一个。工厂方法让类把实例化推迟到子类**。

通用类图为：

![工厂方法通用类图](http://occl9k36n.bkt.clouddn.com/2017_03_27_FactoryMethodDiagram.png)


一些问题的解答：

(1)利用字符串传入参数化的类型，是不是有点危险？万一拼错了怎么办？

&emsp;&emsp;的确，这样的问题会导致所谓的运行时错误。避免此类问题的技巧：可以创建代表参数类型的对象和使用静态常量，或者Java中支持的enum类型。

(2)**对比工厂方法和简单工厂之间的区别(非常的重要)**

&emsp;&emsp;工厂方法中的子类确实看上去非常像简单工厂。**简单工厂把全部的事情在一个地方处理完了。然而工厂方法确实创建一个框架，让子类决定如何去实现**。简单工厂的做法可以将对象的创建封装起来，但是简单工厂不具备工厂方法的弹性，因为简单工厂不能改变正在创建的产品。