## DI In Spring (1): Constructor DI and Setter DI

### Explanation

**Start Point**

Depedency Injection (DI) in Spring is provided in three ways. constructor-based DI, setter-based DI, and field-based DI. In these, the contsructor-based DI is the most recommended one and the field based DI is the least recommended. The latter is even thought to be the one which should be avoided. Then, what kind of the pros and cons they have?

**Tackling Curiosity**

1. Constructor-based DI
   
In Spring, the IoC container invokes a constructor. Without using annotations like `@Autowired`, Spring allows the constructor dependency injection of POJO. 

```java
package x.y;

public class ThingOne {

    public ThingOne(ThingTwo thingTwo, ThingThree thingThree) {
        // ...
    }
}
```

```xml
<beans>
    <bean id="beanOne" class="x.y.ThingOne">
        <constructor-arg ref="beanTwo"/>
        <constructor-arg ref="beanThree"/>
    </bean>

    <bean id="beanTwo" class="x.y.ThingTwo"/>

    <bean id="beanThree" class="x.y.ThingThree"/>
</beans>
```

The arguments are resolved in an order by its ocurrence in default. The `ThingOne` class above requires two parameters as mandatory arguments. Here, the word 'mandatory' means that instantiation without the valid parameters cannot be done. The type of `beanTwo` and `beanThree`are easily determined.

it will be helpful how the class of the bean is expressed. `x.y.ThingOne` means that `ThingOne` class in package `x.y`.

```xml
<bean id="exampleBean" class="examples.ExampleBean">
    <constructor-arg type="int" value="7500000"/>
    <constructor-arg type="java.lang.String" value="42"/>
</bean>
```

```xml
<bean id="exampleBean" class="examples.ExampleBean">
    <constructor-arg index="0" value="7500000"/>
    <constructor-arg index="1" value="42"/>
</bean>
```

If the constructor includes any simple type, the explicit type specfication would be needed. Also, the `index` attributes can be used to determine the right place of the argument. These show how to avoid the ambigiuities among arguments. The `@ConstructorProperties` notation helps the constructior based DI, too. 

```java
package examples;

public class ExampleBean {

    // Fields omitted

    @ConstructorProperties({"years", "ultimateAnswer"})
    public ExampleBean(int years, String ultimateAnswer) {
        this.years = years;
        this.ultimateAnswer = ultimateAnswer;
    }
}
```

2. Setter-based DI

As the name shows, Setter-based DI uses calling setter methods. In the process, the "no-argument" constructor or static factory method is invoked first.

```java
public class SimpleMovieLister {

	// the SimpleMovieLister has a dependency on the MovieFinder
	private MovieFinder movieFinder;

	// a setter method so that the Spring container can inject a MovieFinder
	public void setMovieFinder(MovieFinder movieFinder) {
		this.movieFinder = movieFinder;
	}

	// business logic that actually uses the injected MovieFinder is omitted...
}
```

What notable is that the `BeanDefinition` is the format in configuring dependencies. The class would be another deep dive topic, so this time will not be adequate. Instead, the frequently used annotations and XML bean defintions are internally converted to the `BeanDefinition`.

### Furthermore

The two DI styles can be used together. The constructor DI would be used for mandatory dependencies. The setter DI would be used for optional dependencies. As the features with constructor DI ensures not-null and immutable, it gets used in the mandatory ones.

Spring official docs say that the `@Autowired` makes the applied part required one. As it removes the meaning of the 'optional', the programmatic validation might be a better choice. It means that setter methods DI is only for optional dependencies. If not, the not-null check should be executed previously. 

### References

