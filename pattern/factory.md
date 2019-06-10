# 工厂模式

## 简单工厂

相信大家都写过类似的代码
```java
    Duck duck;
    if(picnic){
        duck = new MallardDuck();
    }else if(hunting){
        duck = new DecoyDuck();
    }else if(){
        duck = new RubberDuck();
    }
```
这里有一些要实例化的具体类，究竟实例化哪个类，要在运行时由一些条件来决定，一旦判断条件有变化，必须打开这块代码进行检查和修改。通常这样修改过的代码将造成部分系统更难维护和更新，也更容易出错。

所以，遇到这样的问题时，该怎么办呢？我们应该"找出会变化的方面，把它们从不变的部分分离出来"。

下面我们来看下这段代码。
```java
public class JianbingShop {

    String jianbingName ;

    JianbingShop(String jianbingName){
        this.jianbingName = jianbingName;
    }

    public void orderJianbing(){
        Jianbing jianbing = null;
        if(jianbingName.equals("鸡蛋")){
            jianbing = new JidanJianbing();
        }else if(jianbingName.equals("牛肉")){
            jianbing = new NiurouJianbing();
        }else if(jianbingName.equals("培根")){
            jianbing = new PeigenJianbing();
        }else{
            System.out.println("老铁，做不了啊");
        }
        System.out.println("老姜点了个"+jianbing.toString());
        //准备材料
        jianbing.prepare();
        //做煎饼
        jianbing.fabrication();
        //打包
        jianbing.encasement();
    }
}
```
某一天，我们开了一个煎饼果子店，需要根据不同的客户的口味来做不同的煎饼，以前我们只会做鸡蛋、牛肉和培根口味的，突然有一天有个客户说他想吃加烤肠的，并且培根太贵不赚钱，不打算做了，这个时候，大家应该知道哪块是会变的，哪块是不会变的。

那么现在我们应该怎么做呢？

首先，我们应该把创建对象的代码从orderJianbing()方法中抽离。

然后把这部分代码搬到另一个对象中，我们暂且叫它SimpleJianbingFactory，这个新对象只管如何创建煎饼。如果任何对象想要创建煎饼，找它就对了。

```java
public class SimpleJianbingFactory {
    public Jianbing createJianbing(String jianbingName){
        if(jianbingName.equals("鸡蛋")){
            return new JidanJianbing();
        }else if(jianbingName.equals("牛肉")){
            return new NiurouJianbing();
        }else if(jianbingName.equals("培根")){
            return new PeigenJianbing();
        }else{
            System.out.println("老铁，" + jianbingName + "煎饼做不了啊");
            return null;
        }
    }
}
```
问：这么做有什么好处呢？只不过把问题从一个对象搬到了另一个对象罢了，问题依然存在。
答：别忘了，SimpleJianbingFactory可能有很多地方在调用，而不止一个地方在调，当需要改变实现时，只需要改正和一个类即可。同时，我们也把具体实例化的过程从客户代码中删除！

那么客户代码修改成什么样了呢？

```java
public class JianbingShop {
    
    SimpleJianbingFactory simpleJianbingFactory;
    
    public JianbingShop(SimpleJianbingFactory simpleJianbingFactory){
        this.simpleJianbingFactory = simpleJianbingFactory;
    }

    public void orderJianbing(String jianbingName){
        Jianbing jianbing = simpleJianbingFactory.createJianbing(jianbingName);
        System.out.println("老姜点了个"+jianbing.toString());
        jianbing.prepare();
        jianbing.fabrication();
        jianbing.encasement();
    }

}
```

这就是一个"简单工厂"的实现。简单工厂其实并不是一个设计模式，反而更像是一种编码习惯。但是不要因为简单工厂不是一个"真正的"模式，就忽略了它的用法。

## 工厂方法模式

哎，我们的煎饼果子摊开的还不错，突然有一天，老姜说，我也要加盟，桓齐你在牡丹园开，我在北苑也开一家。既然是加盟，做法肯定还是用你之前的做法，只是我不卖火腿的煎饼，我要卖烤肠的。

那么老姜说的做法不变是哪块不变呢？制作煎饼的流程不变，只是加的东西不一样了。

```java
    jianbing.prepare();
    jianbing.fabrication();
    jianbing.encasement();
```

我们前面用简单工厂实现了根据需要创建不同的煎饼，但是现在跟之前不一样了，老姜非得做烤肠的，我还不想做，那怎么办呢。分家！

我们先来修改一下原来的店：

```java
public abstract class JianbingShop {

    public abstract Jianbing createJianbing(String jianbingName);

    public void orderJianbing(String jianbingName){
        Jianbing jianbing = createJianbing(jianbingName);

        if(jianbing == null){
            return;
        }
        System.out.println("老姜点了个"+jianbing.toString());
        jianbing.prepare();
        jianbing.fabrication();
        jianbing.encasement();
    }
}
```

大家注意到，我们把类修改为抽象类了，为什么这样改后面再说。制作煎饼的流程不变，只是获取煎饼类型的地方用一个抽象方法替代。

既然要分，就分的彻底一点，我们把店分成了牡丹园店和北苑店。

```java
class MudanyuanJianbingShop extends JianbingShop{

    @Override
    public Jianbing createJianbing(String jianbingName) {
        if(jianbingName.equals("鸡蛋")){
            return new JidanJianbing();
        }else if(jianbingName.equals("牛肉")){
            return new NiurouJianbing();
        }else if(jianbingName.equals("培根")){
            return new PeigenJianbing();
        }else if(jianbingName.equals("火腿")){//火腿多好吃
            return new HuotuiJianbing();
        }else{
            System.out.println("老铁，" + jianbingName + "煎饼做不了啊");
            return null;
        }
    }
}

class BeiyuanJianbingShop extends JianbingShop{

    @Override
    public  Jianbing createJianbing(String jianbingName){
        if(jianbingName.equals("鸡蛋")){
            return new JidanJianbing();
        }else if(jianbingName.equals("牛肉")){
            return new NiurouJianbing();
        }else if(jianbingName.equals("培根")){
            return new PeigenJianbing();
        }else if(jianbingName.equals("烤肠")){//老姜非得作
            return new KaochangJianbing();
        }else{
            System.out.println("老铁，" + jianbingName + "煎饼做不了啊");
            return null;
        }
    }
}

```
原本由一个对象负责所有对象的实例化，现在通过JianbingShop的一些转变，变成了一群子类来负责实例化。我们能够看出**工厂方法模式**咏来处理对象的创建，并将这样的行为封装在子类中。这样程序中关于父类的代码就和子类对象创建代码解耦了。

我们就用煎饼店来看下工厂模式的类图

![](../images/pattern/factory_method_uml.png)

**工厂方法模式**（Factory Method Pattern）的定义：在基类中定义创建对象的一个接口，让子类决定实例化哪个类。工厂方法让一个类的实例化延迟到子类中进行。

从类图中我们可以看到，抽象的工厂类提供了一个创建对象的方法的接口，也成为"工厂方法"。

现在，杰明看老姜干的风风火火，想在西直门也开一家店，应该怎么做？