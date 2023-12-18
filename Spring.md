

 

 The org.springframework.context.ApplicationContext interface represents the Spring IoC container and is responsible for instantiating, configuring, and assembling the beans.

ApplicationContext
* ClassPathXmlApplicationContext 
* FileSystemXmlApplicationContext.


BeanEntry

 BeanDefinition 

 BeanDefinitionMap

 BeanDefinitionReader


 PostProcessor，针对不同操作对象
 * BeanFactoryPostProcessor：
   * PlaceholderConfigurerSupport
   * BeanDefinitionRegistryPostProcessor
 * BeenPostProcessor

ApplicationContext继承了BeanFactory

> @Controller 控制器（注入服务）
> @Servicice  服务（注入DAO）
> @Repository DAO
> @Component 把普通的POJO实例化到Spring容器，相当于配置文件中been



@import
@CompoentScan


ConfigurableListableBeanFactory

 * 接口  能力，。自上向下
 * 抽象类： 自下向上

Spring支持如下5种作用域：
* singleton：单例模式，在整个Spring IoC容器中，使用singleton定义的Bean将只有一个实例
* prototype：原型模式，每次通过容器的getBean方法获取prototype定义的Bean时，都将产生一个新的Bean实例
* request：对于每次HTTP请求，使用request定义的Bean都将产生一个新实例，即每次HTTP请求将会产生不同的Bean实例。只有在Web应用中使用Spring时，该作用域才有效
* session：对于每次HTTP Session，使用session定义的Bean豆浆产生一个新实例。同样只有在Web应用中使用Spring时，该作用域才有效
* globalsession：每个全局的HTTP Session，使用session定义的Bean都将产生一个新实例。典型情况下，仅在使用portlet context的时候有效。同样只有在Web应用中使用Spring时，该作用域才有效


 1. 实例化:在堆空间中申请空间，并通过反射中创建对象。createBeanInstance
 2. 初始化：
 　自定义属性赋值 populateBeanset
 　容器对象属性赋值 invokeAwareMethods()
 
 　两类对象：自定义对象和容器对象
 3. 
 4. 