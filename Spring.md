

 ApplicationContext


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