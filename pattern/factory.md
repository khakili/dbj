相信大家都写过类似的代码
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
        jianbing.prepare();
        jianbing.fabrication();
        jianbing.encasement();
    }

    public static void main(String[] args) {
        JianbingShop jianbingShop = new JianbingShop("鸡蛋");
        jianbingShop.orderJianbing();
    }

}
```







工厂模式（Factory Method Pattern）的定义：在基类中定义创建对象的一个接口，让子类决定实例化哪个类。工厂方法让一个类的实例化延迟到子类中进行。