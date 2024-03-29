#  设计模式



###  装饰器模式

 1. 定义接口

    ```java
    public interface Component {
        void doSomeThing();
    }
    ```

2. 具体构建角色

    ```java
    public class ConcreateCompnent implements Component {
        @Override
        public void doSomeThing() {
            System.out.println("A功能");
        }
    }
    ```

3. 声明装饰器

    ```java
    public class Decorator implements Component {
        private Component component;
    
        Decorator(Component component) { 
            this.component = component;
        }
        @Override
        public void doSomeThing() {
            component.doSomeThing();
        }
    }
    
    ```

4. 装饰类的具体实现

    ```java
    public class ConcratorDecorator1 extends Decorator {
    
        ConcratorDecorator1(Component component) { //必须传入具体构建角色才能够装饰
            super(component);
    
        }
        @Override
        public void doSomeThing() { //在保留父类方法的同时拓展新的方法
            super.doSomeThing();
            this.doAnotherThing();
        }
        public void doAnotherThing() { //拓展的新方法
            System.out.println("功能B");
        }
    }
    
    public class ConcratorDecorator2 extends Decorator {
        ConcratorDecorator2(Component component) {
            super(component);
        }
        @Override
        public void doSomeThing() {  
            super.doSomeThing();
            this.doAnotherThing();
    
        }
        public void doAnotherThing() {
            System.out.println("功能C");
        }
    }
    
    ```

5. Test

    ```java
    Component component = new ConcratorDecorator2(new ConcratorDecorator1(new ConcreateCompnent())); //具体构建对象new ConreateComponent（）同时具有了装饰器1和在装饰器2所提供的拓展方法
    component.doSomeThing(); 
    ```


## 单例模式

1. 双重检查模式(线程安全)

   ```java
   class Singleton {
       private volatile static Singleton singleton;
   
       //不允许直接被外部调用构造方法
       private Singleton() {
   
       }
       public static Singleton getSingleton(){
           if (singleton == null) {
               synchronized (Singleton.class) {
                   if (singleton == null) {
                       singleton = new Singleton();
                   }
               }
           }
           return singleton;
       }
   
   }
   ```

2. 静态内部类单例模式

   ```java
   class Singleton {
       private Singleton() {
   
       }
   
       public static Singleton getInstance() {
           return SingletonHolder.instance;
       }
   
       private static class SingletonHolder {
           private static final Singleton instance = new Singleton();
       }
   }
   ```

   

3. 枚举单例

   ```java
   enum Sigleton{
       Instance
   }
   ```

****

### 模板方法

**优点：** 1、封装不变部分，扩展可变部分。 2、提取公共代码，便于维护。 3、行为由父类控制，子类实现。

**缺点：**每一个不同的实现都需要一个子类来实现，导致类的个数增加，使得系统更加庞大。

**使用场景：** 1、有多个子类共有的方法，且逻辑相同。 2、重要的、复杂的方法，可以考虑作为模板方法。

**注意事项：**为防止恶意操作，一般模板方法都加上 final 关键词。

```java
public abstract class TemplateMethod {

    public final void print(String message) {
        System.out.println("-----------");
        wrapPrint(message);
        System.out.println("-----------");
    }
    protected abstract void wrapPrint(String message);
}

//------------------------------
public class Test extends TemplateMethod {
    protected void wrapPrint(String message) {
        System.out.println(message+"这是模板方法的实现");
    }
    public static void main(String[] args) {
        new Test().wrapPrint("Hello World");
    }
}
```



**持续补充中***

