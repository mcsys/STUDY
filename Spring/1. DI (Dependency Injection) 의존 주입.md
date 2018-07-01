# DI (Dependency Injection) 의존 주입

A라는 객체가 있는데 A객체에 setter(), construct()를 사용해서 직접 New로 생성하지 않고

A라는 객체안에 B와 C를 받을 필드를 만들어 놓고 setter와 construct를 이용해서 B와 C를 받는다.

즉, B/C 객체는 외부에서 생성하여 A객체에 넣어주는 것을 DI(Dependency Injection)이라 한다.

DI는 외부에서 의존하는 객체를 만들어 주입한다. 라는 의미다. 



# IOC 컨테이너

위와 같이 외부에서 객체를 만들어 주입(도킹)하는 객체들이 모였는 있는 것을 IOC 컨테이너라고 한다.

Spring은 부품을 생성하고 조립하는 라이브러리 집합체라고 생각하면 된다. (DI, IOC 컨테이너)



# bean 객체 생성

~~~java
String configLocation = "classpath:applicationCTX.xml";
AbstractApplicationContext ctx = new GenericXmlApplicationContext(configLocation);
MyCalculator myCalculator = ctx.getBeen("myCalculator", MyCalculator.class)
~~~

외부에서 만들어서 객체를 주입하는 방법이다. (Dependency Injection)

xml에서 bean을 가져올 때 다음과 같이 작성한다. 



~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

	<bean id="calculator" class="com.javalec.ex.Calculator" />
	
	<bean id="myCalculator" class="com.javalec.ex.MyCalculator">
		<property name="calculator">
			<ref bean="calculator"/>
		</property>
		<property name="firstNum" value="10" />
		<property name="secondNum" value="2"></property>
	</bean>

</beans>

~~~

xml에다가 bean이라는 객체를 하나 생성하고 id값과 class값을 준다.

~~~~xml
<bean id="calculator" class="com.javalec.ex.Calculator" />
~~~~

이 방법은 Java 코드에서 다음과 같다.

~~~java
myCalculator.setCalculator(new Calculator());
~~~



프로퍼티는 xml에서 다음과 같이 설정한다.

~~~xml
<property name="calculator">
    <ref bean="calculator"/>
</property>
<property name="firstNum" value="10" />
<property name="secondNum" value="2"></property>
~~~

Value 값은 FirstNum에 10이라는 값과 secondNum에는 2를 주입한다.

**위 처럼 주입될 수 있는 이유는 MyCalculator에 firstNum, secondNum의 Setter가 있어서 가능한거다.**



이 방법은 java 코드에서 다음과 같다.

~~~java
Calculator calculator;
private int firstNum;
private int secondNum;

myCalculator.setFirstNum(10);
myCalculator.setSecondNum(2);
~~~



**Spring이 적용되지 않은 클래스**

~~~java
MyCalculator myCalculator = new MyCalculator();
myCalculator.setCalculator(new Calculator());

myCalculator.setFirstNum(10);
myCalculator.setSecondNum(2);

myCalculator.add();
myCalculator.sub();
myCalculator.mul();
myCalculator.div();
~~~



**spring이 적용된 클래스**

~~~java
String configLocation = "classpath:applicationCTX.xml";
AbstractApplicationContext ctx = new GenericXmlApplicationContext(configLocation);
MyCalculator myCalculator = ctx.getBean("myCalculator", MyCalculator.class);

myCalculator.add();
myCalculator.sub();
myCalculator.mul();
myCalculator.div();
~~~



~~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

	<bean id="bmiCalcaulator" class="com.javalec.ex.BMICalculator">
		<property name="lowWeight">
			<value>18.5</value>
		</property>
		<property name="normal">
			<value>23</value>
		</property>
		<property name="overWeight">
			<value>25</value>
		</property>
		<property name="obesity">
			<value>30</value>
		</property>
	</bean>
	
	<bean id="myInfo" class="com.javalec.ex.MyInfo">
		<property name="name">
			<value>홍길동</value>
		</property>
		<property name="height">
			<value>187</value>
		</property>
		<property name="weight">
			<value>84</value>
		</property>
		<property name="hobbys">
			<list>
				<value>수영</value>
				<value>요리</value>
				<value>독서</value>
			</list>
		</property>
		<property name="bmiCalculator">
			<ref bean="bmiCalcaulator"/>
		</property>
	</bean>

</beans>
~~~~

**의존 주입은 xml 말고도 java 파일로도 가능하다!**



생성자를 통해서 의존 주입을 할 수 있다.

~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

	<bean id="student1" class="com.javalec.ex.Student">
		<constructor-arg>
			<value>홍길동</value>
		</constructor-arg>
		<constructor-arg>
			<value>10살</value>
		</constructor-arg>
		<constructor-arg>
			<value>3학년</value>
		</constructor-arg>
		<constructor-arg>
			<value>20번</value>
		</constructor-arg>
	</bean>
	
	<bean id="student2" class="com.javalec.ex.Student">
		<constructor-arg value="홍길동" />
		<constructor-arg value="9살" />
		<constructor-arg value="2학년" />
		<constructor-arg value="10번" />
	</bean>
	
	<bean id="studentInfo" class="com.javalec.ex.StudentInfo">
		<constructor-arg>
			<ref bean="student1" />
		</constructor-arg>
	</bean>
	
</beans>
~~~

~~~~xml
<constructor-arg value="홍길동" />
<constructor-arg value="9살" />
<constructor-arg value="2학년" />
<constructor-arg value="10번" />
~~~~

