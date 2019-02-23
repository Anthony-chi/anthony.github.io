springboot的maven pom.xml配置文件

首先配置文件里最上面的是项目的parent标签：
springboot的父项目：
<parent>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-parent</artifactId>
	<version>1.5.19.RELEASE</version>
	<relativePath/> <!-- lookup parent from repository -->
</parent>

点进去可以看到它的父项目：
<parent>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-dependencies</artifactId>
	<version>1.5.19.RELEASE</version>
	<relativePath>../../spring-boot-dependencies</relativePath>
</parent>

回到最初的pom.xml第一依赖：
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-web</artifactId>
</dependency>

spring-boot-starter是springboot的场景启动器：帮我们导入了web模块正常运行所依赖的组件；

spring boot将所有的功能场景都抽取出来，做成一个个的starters（启动器），只需要在项目里引入这些starter相关场景的所有依赖都会导入进来。要用什么功能，就导入什么场景启动器。

@SpringBootApplication：spring boot应用标注在某个类上说明这个类是SpringBoot的主配置类，SpringBoot就应该运行这个类的main方法类启动SpringBoot应用。

SpringBootApplication主类包含如下注解：
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(excludeFilters = {
		@Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
		@Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })
public @interface SpringBootApplication {

1、@Target(ElementType.TYPE)

2、@Retention(RetentionPolicy.RUNTIME)

3、@Documented

4、@Inherited

5、@SpringBootConfiguration
@SpringBootConfiguration:Spring Boot的配置类：
标注在某个类上，表示这是一个Spring Boot的配置类

	@Configuration：作为@SpringBootConfiguration注解里面的注解，配置类上来就标注这个注解
	配置类---配置文件；配置类也是容器中的一个组件；@Component

6、@EnableAutoConfiguration
@EnableAutoConfiguration：开启自动配置功能
以前我们需要配置的东西，Spring Boot帮我们自动配置；
@EnableAutoConfiguration告诉SpringBoot开启自动配置功能，这样自动配置才能生效
在这个注解类里，有如下注解：
@SuppressWarnings("deprecation")
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@AutoConfigurationPackage
@Import(EnableAutoConfigurationImportSelector.class)
public @interface EnableAutoConfiguration {

在这个注解类里，有如下注解：
@AutoConfigurationPackage：自动配置包

在这个package类里，有@Import注解：
@Import(AutoConfigurationPackage.Registar.class);
这个注解是Spring底层注解@Import，他的作用是给容器导入一个组件，导入的组件由AutoConfigurationPackage.Registrar.class完成注册和操作;
将主配置类（@SpringBootApplication标注的类）的所在包及下面所有的子包里面的所有组件扫描到Spring容器。

@EnableAutoConfiguration注解下面还有@Import注解
@Import(EnableAutoConfigurationImportSelector.class)
他的作用是给容器导入组件，EnableAutoConfigurationImportSelector告诉我们要导入那些组件，将所有导入的组件以全类名的方式返回，这些组件就会被添加到容器中，他会给容器中导入非常多的自动配置类（***autoConfiguration）。就是给容器中导入这个场景所需要的所有组件，并配置好这些组件。
 
有了自动配置类，就免去了我们手动编写功能注入的配置文件的工作。
怎么拿这些配置文件呢：
SpringFactoriesLoader.loadFactoryNames(EnableAutoConfiguration.class,classLoader);
从类路径下的META-INF/spring.factories中获取EnableAutoConfiguration指定的值，将这些值作为自动配置类导入到容器中，自动配置类就生效了，就帮我们进行自动配置工作了。以前我们需要自己配置的东西，自动配置类帮我们做了。其实以前配置的东西一个都不能少，只是springboot帮我们做了。J2ee整体整合解决方案和自动配置都在C:\Users\zalta\.m2\repository\org\springframework\boot\spring-boot-autoconfigure\1.5.19.RELEASE\spring-boot-autoconfigure-1.5.19.RELEASE.jar!\org\springframework\boot\autoconfigure这个路径下

7、@ComponentScan(excludeFilters = {
		@Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
		@Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })



