### spring 容器

Spring IOC容器读取Bean配置创建Bean实例之前，必须对它进行实例化。只有在容器实例化后，才可以从IOC容器中获取Bean实例并使用。

Spring提供了两种类型的IOC容器实现：

—BeanFactory：IOC容器的基本实现；

—ApplicationContext：提供了更多的高级特性，是BeanFactory的子接口。

几乎所有的应用场合都直接使用ApplicationContext，而非底层的BeanFactory，无论使用何种方式，配置文件时相同。



### 创建Spring的IOC容器

ApplicationContext代表IOC容器;  注解的方式；

——Bean的配置方式：通过全类名（反射）、通过工厂方法（静态工厂方法&实例工厂方法）、FactoryBean

——IOC窗口BeanFactory & ApplicationContext概述

——依赖注入的方式：属性注入；构造器注入

——注入属性值细节

——自动装配

——bean之间的关系：继承；依赖

——bean的作用域：singleton; prototype; WEB; 环境作用域

——使用外部属性文件

——SpEL

——IOC容器中Bean的生命周期

——Spring 4.x新特性：泛型依赖注入



class:bean的全类名，通过反射的方式在IOC容器中创建Bean，所以要求Bean中必须有无参数的构造器。

id:标识容器中的bean，id唯一。

```html
<bean id="helloWorld2" class="com.atguigu.spring.beans.HelloWorld">
	<property name="name2" value="Spring"></property>
</bean>
```



### 从IOC容器获取Bean实例

利用id定位到IOC容器中的bean：

```java
HelloWorld helloWorld =(HelloWorld) ctx.getBean("helloWorld1");
System.out.println(helloWorld);
```



利用类型返回IOC容器中的Bean,但要求IOC容器中必须只能有一个该类型的Bean：

```
HelloWorld helloWorld=ctx.getBean(HelloWorld.class);
System.out.println(helloWorld);
```



使用构造器注入属性值可以指定参数的位置和参数的类型，以区分重载的构造器：

```html
<bean id="car" class="con.atguigu.spring.bean.Car">
	<constructor-arg value="Baoma" index="0" type="java.lang.String"></constructor-arg>
	<constructor-arg value="shanghai" index="1" type="java.lang.String"></constructor-arg>
	<constructor-arg value="240" index="2" type="int"></constructor-arg>
</bean>
```



字面值:可用字符串表示的值,可以通过<value>元素标签或value属性进行注入：

```html
<constructor-arg index="2" type="int">
	<value>100</value>
</constructor-arg>
```



若字面值中包含特殊字符,可以使用<![CDATA[]]>把字面值包裹起来,如下,value值为"<ShangHai^>":

```html
<constructor-arg type="java.lang.String">
	<value><![CDATA[<ShangHai^>]]></value>
</constructor-arg>
```



可以使用property的ref属性建立bean之间的引用关系,如下：

```html
<bean id="person" class="com.atguigu.spring.beans.Person">
	<property name="name" value="Tom"></property>
	<property name="age" value="24"></property>
	<property name="car" ref="car2"></property>
	//还可以写成	<property name="car">
					<ref bean="car2"/>
				</property>
	//内部bean，不能被外部引用,下面的id没有实际意义,可以省略:
	<property name="car">
		<bean id="car3" class="com.atguigu.spring.beans.Car">
			<constructor-arg value="Ford"></constructor-arg>
			<constructor-arg value="Changan"></constructor-arg>
			<constructor-arg value="20000" type="double"></constructor-arg>
		</bean>
	</property>
</bean>
```



Java.util.Map通过<map>标签定义,<map>标签里可以使用多个<entry>作为子标签,每个条目包含一个键和一个值，简单常量使用key和value来定义;Bean引用通过key-ref和value-ref属性定义:

```html
<property name="cars">
	<map>
		<entry key="AA" value-ref="car"></entry>
		<entry key="BB" value-ref="car2"></entry>
	</map>
</property>
```



使用<props>定义java.util.Properties,该标签使用多个<prop>作为子标签,每个<prop>标签必须定义key属性:

```html
<property name="properies">
	<props>
		<prop key="uesr">root</prop>
		<prop key="password">1234</prop>
		<prop key="jdbcUrl">jdbc:mysql:///test</prop>
		<prop kdy="driverClass">com.mysql.jdbc.Driver</prop>
	</prop>
</property>
```



配置单例的集合bean,以供多个bean进行引用,需要导入util命名空间：

```html
<util:list id="cars">
	<ref bean="car"/>
	<ref bean="car2"/>
</util:list>
```



通过p命名空间bean的属性赋值,需要先导入p命名空间,相对于传统的配置方式更加的简洁,如下:

```html
<bean id="person" class="com.atguigu.spring.bean.collection.Person" P:age="30" p:name="Queen" 
p:cars-ref="cars">

</bean>
```



### 自动装配

XML配置里的Bean自动装配,Spring IOC容器可以自动装配Bean,需要做的仅仅是在<bean>的atuowire属性里指定自动装配的模式。

(1)byType(根据类型自动装配):若IOC容器中有多个与目标Bean类型一致的Bean，会产生异常错误。如果bean的id设置为address,另一个设置为address2,则系统会报错。

(2)byName(通过名称自动装配):必须将目标Bean的名称和属性名设置的完全相同，bean和当前的setter风格的属性名进行自动匹配，若bean的id为address,setter的函数名为setAddress()即可匹配,如果将id改为address2则不能进行匹配。
		(3)constructor(通过构造器自动装配):当Bean中存在多个构造器时,此种自动装配方式将会很复杂,不推荐使用。

一般情况下，在实际的项目中很少使用自动装配功能，因为和自动装配功能所带来的好处比起来，明确清晰的配置文档更有说服力一些。



### Bean配置的继承

设置bean的parent属性来指定继承哪个bean的配置。被继承的bean称为父bean,继承这个父bean的bean称为子bean。

子bean从父bean中继承配置，包括bean的属性配置。父bean可以作为配置模板，也可以作为bean实例，若只想把父bean作为模板，可以设置bean的abstract属性为true。

并不是bean元素里的所有属性都会被继承,如autowire和abstract等是不会被继承的。

```html
<bean id="address" class="com.atguigu.spring.atuowire.Address" p:city="Beijing" P:street="WuDaoKou"></bean>

<bean id="address2" p:city="Beijing" p:street=DaZhongSi" parent="address"></bean>
```

上面第二个bean与第一个bean有相同的class和city属性。



### Bean依赖

Spring允许用户通过depends-on属性设定Bean前置依赖的Bean,前置依赖的Bean会在本Bean实例化之前创建好。如果前置依赖于多个Bean,则可以通过逗号、空格的方式配置Bean的名称。

```html
<bean id="car" class="com.atguigu.spring.beans.autowire.Car" p:brand="Audi" p:price="30000"></bean>

<bean id="person class="com.atguigu.spring.beans.atuowire.Person" p:name="Tom" p:address-ref="address2" depends-on="car"></bean>
```



### Bean的作用域

使用bean 的scope属性来配置bean的作用域。

singleton：默认值，容器初始化时创建bean实例。在整个容器的生命周期内只创建这一个bean，单例的。

prototype：原型的，容器初始化时不创建bean的实例，而在每次请求时都创建一个新的Bean实例，并返回。

```html
<bean id="car" class="com.atguigu.spring.beans.atuowire.Car" scope="singleton">
	<property name="brand" value="Audi"></property>
    <property name="price" value="30000"></property>
</bean>
```

当在主程序写如下语句时，由于设置了scope为“singleton"，则会输出true。如果将bean中的scope设置为”prototype"，则输出会为false。

```java
public class Main{
    public static void main(String[] args){
        ApplicationContext ctx=new ClassPathXmlApplicationContext("beans-scope.xml");
        Car car=(Car)ctx.getBean("car");
        Car car2=(Car)ctx.getBean("car");
        
        System.out.println(car==car2);
    }
}
```



### 使用外部属性文件

Spring提供了一个PropertyPlaceholderConfigurer的BeanFactory后置处理器，这个处理器允许用户将Bean配置的部分内容外移到属性文件中。可以在Bean配置文件里使用形式为${var}的变量，PropertyPlaceholderConfigurer从属性文件里加载属性，并使用这些属性来替换变量

Spring还允许在属性文件中使用${propName}，以实现属性之间的引用。

```html
<!--导入属性文件db.properties-->
<context:property-placeholder location="classpath:db.properties"/>

<bean id="dataSource" class="com.mchange.v2.c3p0.ComboPoolDataSource">
	<!--使用外部属性文件的属性-->
    <property name="user" value="${user}"></property>
    <property name="password" value="${password}"></property>
    <property name="driverClass" value="${driverclass}"></property>
    <property name="jdbcUrl" value="${jdbcurl}"></property>
</bean>
```



### Spring表达式语言：SpEL 

Spring表达式语言（简称SpEL）：是一个支持运行时查询和操作对象图的强大的表达式语言。

语法类似于EL：SpEL使用#{...}作为定界符，所有在大框号中的字符都将被认为是SpEL。

通过SpEL可以实现：

​	——通过bean的id对bean进行引用

​	——调用方法以及引用对象中的属性

​	——计算表达式的值

​	——正则表达式的匹配

```html
<bean>
	<property name="city" value="#{Beijing}"></property>
    <property name="street" value="WuDaoKou"></property>
</bean>

<bean id="car" class="com.atguigu.spring.beans.spel.Car">
	<property name="brand" value="Audi"></property>
    <property name="price" value="300000"></property>
    <!--使用Spel引用类的静态属性-->
    <property name="tyrePerimeter" value="#{T(java.lang.Math).PI*80}"></property>
</bean>

<bean id="person" class="com.atguigu.spring.beans.spel.Person">
	<!--使用Spel来应用其他的Bean-->
    <property name="car" value="#{car}"></property>
    <!--使用SpEL来应用其他的Bean-->
    <property name="city" value="#{address.city}"></property>
    <!--在SpEL中使用运算符-->
    <property name="info" value="#{car.price >300000 ? '金领':'白领'}"></property>
</bean>
```



### IOC容器中Bean的生命周期方法

Spring的IOC容器可以管理Bean的生命周期，Spring允许在Bean生命周期的特定点执行定制的任务。

Spring的IOC容器对Bean的生命周期进行管理的过程：

​	——通过构造器或工厂方法创建Bean实例

​	——为Bean的属性设置值和对其他Bean的引用

​	——调用Bean的初始化方法

​	——Bean可以使用了

​	——当容器关闭时，调用Bean的销毁方法

在Bean的声明里设置init-method和destroy-method属性，为Bean指定初始化和销毁方法。

```html
<bean id="car" class="com.atguigu.spring.beans.cycle.Car" init-method="init2" destroy-method="destroy">
	<property name="breand" value="Audi"></property>
</bean>
```



### 创建Bean后置处理器

Bean后置处理器允许初始化方法前后对Bean进行额外的处理。

Bean后置处理器对IOC容器里的所有Bean实例逐一处理，而非单一实例。其典型应用是：检查Bean属性的正确性或根据特定的标准更改Bean的属性。

对Bean后置处理器而言，需要实现Interface BeanPostProcessor接口。在初始化方法被调用前后，Spring将把每个Bean实例分别传递给上述接口的以下两个方法：

​	——postProcessAfterInitialization

​	——postProcessBeforeInitialization



```java
//方法类
public class MyBeanPostProcessor implements BeanPostProcessor{
    @Override
    public Object postProcessBeforeInitialization(Object bean,String beanName) throws BeanException{
        System.out.println("postProcessorBeforeInitialization:"+bean+","+"beanName" );
        return bean;
    }
    
    @Override
    public Object postProcessAfterInitialization(Object bean,String beanName) throws BeanException{
        System.out.println("postProcessorAfterInitialization:"+bean+","+"beanName" );
        return bean;
    }
}
```

对应的配置文件：

```html
<!--配置bean的后置处理器，不需要配置id，容器自动识别是一个BeanPostProcessor-->
<bean class="com.atguigu.spring.beans.cycle.MyBeanPostProcessor"></bean>
```



步骤：

实现BeanPostProcessor接口，并具体提供

Object postProcessBeforeInitialization(Object bean,String beanName):	init-method之前被调用；

Object postProcessAfterInitialization(Object bean,String beanName)：	init-method之后被调用；

的实现

bean: bean实例本身

beanName： IOC容器配置的bean的名字

返回值： 是实际上返回给用户的那个Bean，注意：可以在以上两个方法中修改返回的bean，甚至返回一个新的bean。如下：

```java
//方法类
public class MyBeanPostProcessor implements BeanPostProcessor{
    @Override
    public Object postProcessBeforeInitialization(Object bean,String beanName) throws BeanException{
        System.out.println("postProcessorBeforeInitialization:"+bean+","+"beanName" );
        return bean;
    }
    
    @Override
    public Object postProcessAfterInitialization(Object bean,String beanName) throws BeanException{
        System.out.println("postProcessorAfterInitialization:"+bean+","+"beanName" );
        Car car=new Car();
        car.setBrand("Ford");
        return bean;
    }
}
```



### 调用静态工厂方法创建Bean

调用静态工厂方法创建Bean是将对象创建的过程封装到静态方法中。当客户端需要对象时，只需简单地调用静态方法，而不用关心创建对象的细节。

要声明通过静态方法创建的Bean，需要在Bean的class属性里指定拥有该工厂的方法的类，同时在factory-method属性里指定工厂方法的名称。最后，使用<constructor-arg>元素为该方法传递方法参数。

```java
//静态工厂方法类StaticCarFactory.java：直接调用某一个类的静态方法就可以返回Bean的实例
public class StaticCarFactory{
    private static Map<String,Car> cars=new HashMap<String,Car>();
    static {
        cars.put("audi",new Car("audi",300000));
        cars.put("ford",new Car("ford",400000));
    }
    
    //静态工厂方法
    public static Car getCar(String name){
        return cars.get(name);
    }
}
```

```html
<!--beans-factory.xml-->
<!-- 通过静态工厂方法来配置bean，注意不是配置静态工厂方法实例，而是配置bean实例-->
<!--
	class属性：指向静态工厂方法的全类名
	factory-method:指向静态工厂方法的名字
	constructor-arg:如果工厂方法需要传入参数，则使用constructor-arg来配置参数
-->
<bean id="car1" class="com.atguigu.spring.beans.factory.StaticCarFactory" factory-method="getCar">
	<constructor-arg value="audi"></constructor-arg>
</bean>
```

```java
//主程序Main.java
public class Main{
    public class void main(String[] args){
        ApplicationContext ctx=new ClassPathXmlApplicationContext("beans-factory.xml");
        Car car1=(Car)ctx.getBean("car1");
        System.out.println(car1);
    }
}
```



### 调用实例工厂方法创建Bean

实例工厂方法：将对象的创建过程封装到另外一个对象实例的方法里。当客户端需要请求对象时，只需要简单的调用该实例方法而不需要关心对象的创建细节。

```java
//实例工厂方法InstanceCarFactory.java，即先需要创建工厂本身，再调用工厂的实例方法来返回bean的实例
public class InstanceCarFactory{
    private Map<String,Car> cars=null;
    
    public InstanceCarFactory{
        cars=new HashMap<String,CAr>();
        cars.put("audi",new Car("audi",300000));
        cars.put("ford",new Car("ford",400000));
    }
    
    public Car getCar(String brand){
        return cars.get(brand);
    }
}
```

```html
<!--通过实例工厂方法来配置bean-->
<bean id="carFactory" class="com.atguigu.spring.beans.factory.InstanceCarFactory"></bean>

<!--通过实例工厂方法来配置bean-->
<!--
	factory-bean属性：指向实例工厂方法的bean
	factory-method:指向实例工厂方法的名字
	constructor-arg:如果工厂方法需要传入参数，则使用constructor-arg来配置参数
-->

<bean id="car2" factory-bean="carFactory" factory-method="getCar">
	<constructor-arg value="ford"></constructor-arg>
</bean>
```

实例工厂方法的主程序写法与上面一致



### FactoryBean实例

在配置bean时，如果需要用到IOC容器中的其它bean，通过FactoryBean是最合适的。

```java
//CarFactoryBean.java，里面一般都只包含以下三种方法
//自定义的FactoryBean需要实现FactoryBean接口
public class CarFactoryBean impliments CarFactoryBean<Car>{
    private Sring brand;
    public void setBrand(Sring brand){
        this.bread=brand;
    }
    
    //返回bean的对象
    @Override
    public Car getObject() throws Exception{
        return new Car("BMW",500000);
    }
    
    //返回的bean
    @Override
    public Class<?> getObjectType(){
        return Car.class;
    }
    
    @Override
    public boolean isSingliton(){
        return false;
    }
}
```

```html
<!--通过FactoryBean来配置Bean的实例
	class:指向FactoryBean的全类名
	property:配置FactoryBean的属性

	但实际返回的实例却是FactoryBean的getObject()方法返回的实例！
-->
<bean id="car" class="com.atguigu.spring.beans.factorybean.CarFactoryBean">
	<property name="brand" value="BMW"></property>
</bean>
```

在主程序中正常创建即可。



### 基于注解的方式配置Bean

组件扫描：Spring能够从classpath下自动扫描，侦测和实例化具体特定注解的组件。

特定组件包括：

​	@Component：基本注解，标识了一个受Spring的组件

​	@Respository：标识持久层组件

​	@Service：标识服务层（业务层）组件

​	@Controller：标识表现层组件

对于扫描到的组件，Spring有默认的命名策略：使用非限定类名，第一个字母小写。也可以在注解中通过value属性值标识组件的名称。



当在组件类上使用了特定的注解之后，还需要在Spring的配置文件中声明 <context: component-scan>:

​	——base-package属性指定一个需要扫描的基类包，Spring容器将会扫描这个基类包里及其子包中的所有类。

​	——当需要扫描多个包时，可以使用逗号分隔。

​	——如果仅希望扫描特定的类而非基包下的所有类，可使用resource-pattern属性过滤特定的类，示例：

```html
<context:component-scan base-package="com.atguigu.spring.beans" resource-pattern="autowire/*.class"/>
```

​	——<context: include-filter>子节点表示要包含的目标类

​	——<context: exclude-filter>子节点表示要排除的目标类

​	——<context: component-scan>下可以拥有若干个<context: include-filter>和<context: exclude-filter>子节点



<context: include-filter>和<context: exclude-filter>子节点支持多种类型的过滤表达式：

​	——annotation:所有标注了XxxAnnotation的类，该类型采用目标类是否标注了某个注解进行过滤。

​	——assignable:所有继承或扩展XxxService的类，该类型采用目标类是否继承或扩展某个特定类进行过滤。

```html
<!-- context:exclude-filter子节点指定排除哪些指定表达式的组件-->
<!-- context:include-filter子节点指定包含哪些表达式的组件，该子节点需要use-default-filter配合使用-->
<context:component-scan base-package="com.atguigu.spring.beans.annotation" use-default-filters="false">
    <!--
	<context:exclude-filter type="annotation" 			expression="org.springframework.stereotype.Repository"/>
	-->
    
    <!--
	<context:include-filter type="annotation" expression="org.springframework.stereotype.Repository/">
	-->
    
    <context:include-filter type="assignable" expression="com.atguigu.spring.beans.annotation.repository.UserRepository"/>
</context:component-scan>
```



使用@Autowired自动装配Bean

@Autowired注解自动装配具有兼容类型的单个Bean属性

​	——构造器，普通字段（即便是非public），一切具有参数的方法都可以应用@Autowired注解。

​	——默认情况下，所有使用@Autowired注解的属性都需要被设置。当Spring找不到匹配的Bean装配属性时，会抛出异常，若某一属性允许不被设置，可以设置@Autowired注解的required属性为false。如下

```java
@Autowired(required=false)
private TestObject testObject;
```

​	——默认情况下，当IOC容器存在多个类型兼容的Bean时，通过类型的自动装配将无法工作，此时可以在@Qualifier注解里提供Bean的名称。Spring允许对方法的入参标注@Qualifier已指定注入Bean的名称。



### Spring AOP

AOP（面向切面编程）是一种新的方法论，是对传统OOP（面向对象编程）的补充。AOP的主要编程对象是切面。

切面：横切关注点被模块化的特殊对象

通知：切面必须要完成的工作

目标：被通知的对象

代理：向目标对象应用通知之后创建的对象

连接点：程序执行的某个特定位置：如类的某个方法调用前、调用后、方法抛出异常后等。连接点由两个信息确定：方法表示的程序执行点；相对点表示的方法。例如ArithmeticCalculator#add()方法执行前的连接点，它的执行点为ArithmeticCalculator#add();方位为该方法执行前的位置。

切点：每个类都拥有多个连接点：例如ArithmeticCalculator的所有方法实际上都是连接点，即连接点是程序类中客观存在的事务。AOP通过切点定位到特定的连接点。类比：连接点相当于数据库中的记录，切点相当于查询条件。切点和连接点不是一对一的关系，一个切点匹配多个连接点，切点通过org.springframework.aop.Pointcut接口进行描述，它使用类和方法作为连接点的查询条件。



AspectJ：Java社区里最完整最流行的AOP框架。

在Spring2.0以上的版本中，可以使用基于AspectJ注解或基于XML配置的AOP。



步骤：

1、加入jar包

2、在配置文件中加入aop的命名空间

3、基于注解的方式

​	——把横切关注点的代码抽象到切面的类中

​	切面首先是一个IOC的bean，即加入@Component注解

​	切面还需要加入@Aspect注解

​	——在类中声明各种通知

​	声明一个方法

​	在方法前加入@Before注解



### 基于注解的方式配置AOP

```java
//LoggingAspect.java
//把这个类声明为一个切面：需要把该类放入到IOC容器中，再声明为一个切面

//当程序存在多个切面时，可以使用@Oder注释指定切面的优先级，值越小优先级越高
@Order(2)
@Aspect
@Component
public class LoggingAspect{
    //前置通知：在目标方法开始之前执行
    //下面execution中的public int可以用“*”表示，代表所有类型；add也可以用“*”表示，代表接口内所有方法。
    //(int,int)可以写成(..)代表任意参数。
    @Before("execution(public int com.atguigu.spring.aop.iml.ArithmeticCalculator.add(int,int))")
    public void beforeMethod(JoinPoint joinPoint){
        String methodName=joinPoint.getSignature().getName();
        List<Object> args=Arrays.asList(joinPoint.getArgs());
        System.out.println("The method "+methodName+" begins with "+args);
    }
    
    //后置通知：在目标方法执行后（无论是否发生异常）执行的通知
    //在后置通知中还不能访问目标方法执行的结果
    @After("execution(* com.atguigu.spring.aop.impl.*.*(int,int))")
    public void afterMethod(JoinPoint joinPoint){
        String methodName=joinPoint.getSignature().getName();
        System.out.println("The method "+ methodName+" ends");
    }
    
    //返回通知：在方法正常结束后执行的代码
    //返回通知是可以访问到方法的返回值的
    @AfterReturning(value="execution(public int com.atguigu.spring.aop.ArithmeticCalculator.*(..))",returning="result")
    public void afterReturning(JoinPoint joinPoint,Object result){
        String methodName=joinPoint.getSignature().getName();
        System.out.println("The method "+ methodName+" ends with"+result);        
    }
    
    //异常通知：在目标方法出现异常时会执行代码。
    //可以访问到异常对象，且可以指定在出现特定异常时再执行通知代码，如将现在的Exception改为对应异常类型。
    @AfterThrowing(value="execution(public int com.atguigu.spring.aop.ArithmeticCalculator.*(..))",throwing="ex")
    public void afterReturning(JoinPoint joinPoint,Exception ex){
        String methodName=joinPoint.getSignature().getName();
        System.out.println("The method "+ methodName+" occurs excetion:"+ex);        
    }
    
    //环绕通知：需要携带ProceedingJoinPoint类型的对象
    //环绕通知类似于动态代理的全过程：ProceedingJointPoint类型的参数可以决定是否执行目标方法
    //且环绕通知必须有返回值，返回值即为目标方法的返回值
    @Around("execution(public int com.atguigu.spring.aop.ArithmeticCalculator.*(..))")
    public Object aroundMethod(ProceedingJoinPoint pjd){
        Object result=null;
        String methodName=pjd.getSignature().getName();
        
        try{
            //前置通知
            System.out.println("The method "+methodName+" begin with "+Arrays.asList(pjd.getArgs()));
            //执行目标方法
            result=pjd.proceed();
            //返回通知
            System.out.println("The method "+methodName+" end with "+result));
        }catch(Throwable e){
            System.out.println("The method "+methodName+" occurs exception:"+e));
            throw new RuntimeException(e);
        }
        //后置通知
        System.out.println("The method "+methodName+" ends");
        return result;
    }
}
```

```html
<!-- 配置自动扫描的包 -->
<context:component-scan base-package="com.atguigu.spring.aop.impl"></context:component-scan>

<!-- 使AspectJ注解起作用：自动匹配的类生成代理对象 -->
<aop:aspectJ-autoproxy></aop:aspectJ-autoproxy>
```



```java
//定义一个方法，用于声明切入点表达式。一般地，该方法再不需要添入其它的代码
//使用@Pointcut来声明切入点表达式
//后面的其它通知直接使用方法名来引用当前的切入点表达式

@Pointcut("execution(public int com.atguigu.spring.aop.ArithmeticCalculator.*(..))")
public void declareJointPointExpression(){}

//引用格式
@Before("declareJointPointExpression()")
```



### 基于配置文件的方式配置AOP

```html
<!-- 配置bean -->
<bean id="arithmeticCalculator" class="com.atguigu.spring.aop.xml.ArithmeticCalculatorImpl"></bean>

<!-- 配置切面的bean -->
<bean id="loggingAspect" class="com.atguigu.spring.aop.xml.loggingAspect"></bean>
<bean id="validationAspect" class="com.atguigu.spring.aop.xml.ValidationAspect"></bean>

<!-- 配置AOP -->
<aop:config>
	<!-- 配置切点表达式 -->
    <aop:pointcut expression="execution(* com.atguigu.spring.aop.xml.ArithmeticCalculator.*(int,int))" id="pointcut"/>
    <!-- 配置切面及通知 -->
    <aop:aspect ref="loggingAspect" order="2">
		<aop:before method="beforeMethod" pointcut-ref="pointcut"/>
        <aop:after method="afterMethod" point-ref="pointcut"/>
        <aop:after-throwing method="afterThrowing" pointcut-ref="pointcut"/>
        <aop:after-returning method="afterReturning" pointcut-ref="poingcut"/>
        
        <!--
			<aop:around method="aroundMethod" pointcut-ref="pointcut"/>
		-->
    </aop:aspect>
    
    <aop:aspect ref="validationAspect" order="1">
    	<aop:before method="validateArgs" pointcut-ref="pointcut"/>
    </aop:aspect>
</aop:config>

```



### Spring对JDBC的支持

为了使JDBC更加易于使用，Spring在JDBC API上定义了一个抽象层，以此建立一个JDBC存取框架

```
//资源文件db.properties
jdbc.user=root
jdbc.password=1230
jdbc.driverClass=com.mysql.jdbc.Driver
jdbc.jdbUrl=jdbc:mysql:///spring4

jdbc.initPoolSize=5
jdbc.maxPoolSize=10
```

```html
<!-- 导入资源文件 -->
<context:property-placeholder location="classpath:db.properties"/>

<!-- 配置C3P0数据源 -->
<bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
	<property name="user" value="${jdbc.user}"></property>
    <property name="password" value="${jdbc.password}"></property>
    <property name="jdbUrl" value="${jdbc.jdbUrl}"></property>
    <property name="driverClass" value="${jdbc.driverClass}"></property>
    
    <property name="initPoolSize" value="${jdbc.initPoolSize}"></property>
    <property name="maxPoolSize" value="${jdbc.maxPoolSize}"></property>
</bean>

<!-- 配置Spring的JdbcTemplate -->
<bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
	<property name="dataSource" ref="dataSource"></property>
</bean>
```

```java
public class JDBCTest{
    private ApplicationContext ctx=null;
    private JdpcTemplate jdpcTemplate;
    
    {
        ctx=new ClassPathXmlApplicationContext("applicationContext.xml");
        jdbcTemplate=(JdbcTemplate)ctx.getBean("jdbcTemplate");
    }
    
    //执行INSERT,UPDATE,DELETE
    public void testUpdate(){
        String sql="UPDATE employees SET last_name = ? WHERE id = ?";
        jdbcTemplate.update(sql."Jack",5);
    }
    
    @Test
    public void testDataSource() throw SQLExctption{
        DataSource dataSource=ctx.getBean(DataSource.class);
        System.out.println(dataSource.getConnection());
    }
}
```



### Spring整合Hibernate

Spring整合Hibernate，需要整合些什么？

​	——有IOC容器来管理Hibernate的SessionFactory

​	——让Hibernate使用上Spring的声明式事务

整合步骤：

1、加入Hibernate

​	——jar包

​	——添加hibernate的配置文件：hibernate.cfg.xml

​	——编写了持久化类对应的.hbm.xml文件

2、加入Spring

​	——jar包

​	——加入Spring配置文件

3、整合

```html
<hibernate-configuration>
	<session-factory>
    	<!--配置hibernate的基本属性-->
        <!-- 1、数据源需配置到IOC容器中，所以在此处不再需配置数据源 -->
        <!-- 2、关联的.hbm.xml也在IOC容器配置SessionFactory实例时在进行配置-->
        <!-- 3、配置hibernate的基本属性：方言，SQL显示及格式化，生成数据表的策略以及二级缓存等-->
        
        <property 	name="hibernate.dialect">org.hibernate.dialect.MySQL5InnoDBDialect</property>
        <property name="hibernate.show_sql">true</property>
        <property name="hibernate.format_sql">true</property>  
        
        <property name="hibernate.hbm2ddl.auto">update</property>
    </session-factory>
</hibernate-configuration>
```

```matlab

```



### Spring MVC

Spring为展现层提供的基于MVC设计理念的优秀的Web框架，是目前最主流的MVC框架之一。

Spring3.0后全面超越Struts2，成为最优秀的MVC框架。SpringMVC通过一套MVC注解，让POJO成为处理请求的控制器，而无须实现任何接口。

编写一个HelloWorld步骤：

​	——加入jar包

​	——在web.xml中配置DispacherServlet

​	——加入Spring MVC的配置文件

​	——编写处理请求的处理器，并标识为处理器

​	——编写视图

```html
<!-- web.xml -->
<!-- 配置DispacherServlet -->
<servlet>
	<servlet-name>springDispacherServlet</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispacherServlet</servlet-class>
    <!-- 配置DispacherServlet的一个初始化参数：配置SpringMVC配置文件的位置和名称 -->
    <!-- 实际上也可以不通过contextConfigLocation来配置SpringMVC配置文件，而使用默认的。默认的配置文件为：/WEB-INF/<servlet-name>-servlet.xml -->
    <init-param>
    	<param-name>contextConfigLocation</param-name>
        <param-value>classpath:springmvc.xml</param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
</servlet>

<servlet-mapping>
	<servlet-name>springDispacherServlet</servlet-name>	
    <url-pattern>/</url-pattern>
</servlet-mapping>
```

```java
//HelloWorld.java
@Controller
public class HelloWorld{
    //使用@RequestMapping注解来映射请求的URL
    //返回值会通过视图解析器解析为实际的物理视图，对于InternalResourceViewResolver视图解析器，会做如下的解析：通过prefix + returnVal + 后缀这样的方式得到实际的物理视图，然后做转发操作，在这里为/WEB-INF/views/success.jsp
    @RequestMapping("/helloworld")
    public String hello(){
        System.out.println("hello world");
        return "successs";
    }
}
```

```html
<!-- springmvc.xml -->
<!-- 配置自定扫描的包 -->
<context:component-scan base-package="com.atguigu.springmvc"></context:component-scan>

<!-- 配置视图解析器：如何把handler方法返回值解析为实际的物理视图 -->
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
	<property name="prefix" value="/WEB-INF/views/"></property>
    <property name="suffix" value=".jsp"></property>
</bean>
```

```html
<!-- index.jsp -->
<a href="helloworld">Hello World</a>
```

```html
<!-- success.jsp -->
<h4>
    Success Page
</h4>
```



Spring MVC使用@RequestMapping注解为控制器指定可以处理哪些URL请求。

在控制器的类定义及方法定义处都可标注@RequestMapping：

​	——类定义处：提供初步的请求映射信息。相对于WEB应用的根目录。

​	——方法处：提供进一步的细分映射信息。相对于类定义处的URL。若类定义处未标注@RequestMapping，则方法处标记的URL相对于WEB应用的根目录。

```java
@RequestMapping("/springmvc")
@Controller
public class SpringMVCTest{
    private static final String SUCCESS="success";
    
    @RequestMapping("/testRequestMapping")
    public String testRequestMapping(){
        System.out.println("testRequestMapping");
        return SUCCESS;
    }
}
```

```html
<!-- index.jsp -->
<a href="springmvc/testRequestMapping">Test RequestMapping</a>
```



DispacherServlet截获请求后，就通过控制器上@RequestMapping提供的映射信息确定请求所对应的处理方法。

@RequestMapping除了可以使用请求URL映射请求外，还可以 使用请求方法、请求参数及请求头映射请求。

@RequestMapping的value、method、params及heads分别表示请求URL、请求方法、请求参数及请求头的映射条件，他们之间是与的关系，联合使用多个条件可让请求映射更加精确化。

```java
//使用method属性来指定请求方式
@RequestMapping(value="/testMethod",method=RequestMethod.POST)
public String testMethod(){
    System.out.println("testMethod");
    return "success";
}
```

params和headers支持简单的表达式：

​	——param1：表示请求必须包含名为param1的请求参数

​	——！param1：表示请求不能包含名为param1的请求参数

​	——param1！=value1：表示请求包含名为param1的请求参数，但其值不能为value1

​	——{"param1=value1","param2"}：请求必须包含名为param1和param2的两个请求参数，且param1参数的值必须为value1



Ant风格资源地址支持3种匹配符

​	——？：匹配文件名中的一个字符

​	——*：匹配文件名中的任意字符

​	——**：匹配多层路径



##### 使用@PathVariable映射URL绑定的占位符

通过@PathVariable可以将URL中占位符参数绑定到控制器处理方法的入参中：URL中的{xxx}占位符可以通过@PathVariable（”xxx")绑定到操作方法的入参中。

```java
@RequestMapping("/testPathVariable/{id}")
public String testPathVariable(@PathVariable("id") Integer id){
    System.out.println("testPathVariable: "+id);
    return "success";
}
```

##### 使用@RequestMapping映射请求

```java
//@RequestParam来映射请求参数
//value值即请求参数的参数名
//required该参数是否必须，默认为true
//defaultValue请求参数的默认值
@RequestMapping(value="/testRequestParam")
public String testRequestParam(@RequestParam(value="username") String un,@RequestParam(value="age",required=false,defaultValue="0") int age){
    System.out.println("testRequesParam,username: "+un+",age: "+age);
    return "success";
}
```

##### 使用@RequestHeader绑定请求报头的属性值

```java
//映射请求头信息，用法同@RequestParam
@RequestMapping("/testRequestHeader")
public String testRequestHeader(@RequestHeader(value="Accept-Language") String al){
    System.out.println("testRequestHeader,Accept-Language: "+al);
    return "success";
}
```

##### 使用@CookieValue绑定请求中的Cookie值 

```java
//@CookieValue:映射一个Cookie值，属性同@RequestParam
@RequestMapping("/testCookieValue")
public String testCookieValue(@CookieValue("JSESSIONID") String sessionID){
    System.out.println("testCookieValue: sessionId: "+ssessionId);
    return "success";
}
```

##### 使用POJO属性名进行自动匹配

```java
//Spring MVC会按请求参数名和POJO属性名进行自动匹配，自动为该对象填充属性值。支持级联属性。
//如：dept.deptId、dept.address.tel等
@RequestMapping("/testPojo")
public String testPojo(User user){
    System.out.println("testPojo: "+user);
    return "success";
}
```

##### 使用Serlvet API作为入参

```java
//可以使用Serlvet原生的API作为目标方法的参数，具体支持以下类型：
//HttpServletRequest
//HttpServletResponse
//HttpSession
//java.security.Principal
//Locale InputStream
//OutputStream
//Reader
//Writer
@RequestMapping("/testServletAPI")
public void testSerlvetAPI(HttpServletRequest request,HttpServletResponse response,Writer out) throws IOException{
    System.out.println("testServletAPI,"+request+","+response);
    out.write("hello springmvc");
}
```



##### 处理模型数据

Spring MVC提供了以下几种途径输出模型数据：

​	——ModelAndView：处理方法返回值类型为ModelAndView时，方法体即可通过该对象添加模型数据

​	——Map及Model：入参为org.springframework.ui.Model、org.springframework.ui.ModelMap或java.uti.Map时，处理方法返回时，Map中的数据会自动添加到模型中。

​	——@SessionAttributes：将模型中的某个属性暂存到HttpSession中，以便多个请求之间可以共享这个属性

​	——@ModelAttributes：方法入参标该注解后，入参的对象就会放到数据模型中



##### 使用ModelAndView

```java
//目标方法的返回值可以是ModelAndView类型，其中可以包含视图和模型信息
//SpringMVC会把ModelAndView的model中数据放入到request域对象中
@RequestMapping("/testModelAndView")
public ModelAndView testModelAndView(){
    String viewName="success";
    ModelAndView modelAndView=new ModelAndview(viewName);
    
    //添加模型数据到ModelAndView中
    modelAndView.addObject("time",new Date());
}
```

##### 使用Map及Model

```java
//目标方法可以添加Map类型（实际上也可以是Model类型或ModelMap类型）的参数
@RequestMapping("/testMap")
public String testMap(Map<String,Object>map){
    System.out.println(map.getClass().getName());
    map.put("names",Arrays.asList("Tom","Jerry","Mike"));
    return "success";
}
```



Rest风格的URL

以CRUD为例：

新增：/order POST

修改：/order/1 PUT

获取：/order/1 GET

删除：/order/1 DELETE

HiddenHttpMethodFilter：浏览器form表单只支持GET与POST请求，而DELETE、PUT等method并不支持，Spring3.0添加了一个过滤器，可以将这些请求转换为标准的http方法，使得支持GET、POST、PUT与DELETE请求。



如何发送PUT请求和DELETE请求呢？

1、需要配置HiddenHttpMethodFilter

```html
<filter>
	<filter-name>HiddenHttpMethodFilter</filter-name>
    <filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>
</filter>

<filter-mapping>
	<filter-name>HiddenHttpMethodFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

2、需要改善POST请求

3、需要在发送POST请求时携带一个name="_method"的隐藏域，值为DELETE或PUT