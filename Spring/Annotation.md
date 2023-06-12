# 一、@SpringBootApplication

# 二、@Autowired、@Resource、@Inject
## 1. 来源
* @Autowired是Spring框架自带注解
* @Resource是JSR250规范实现的，属于javax.annotation包下（java扩展类库的） 
* @Inject是JSR330规范实现的，使用时需要导入javax.inject.Inject包
## 2. 使用范围
* @Autowired：ElementType.CONSTRUCTOR，ElementType.METHOD，ElementType.PARAMETER，ElementType.FIELD（字段、枚举的常量），ElementType.ANNOTATION_TYPE
* @Resource：ElementType.TYPE（接口、类、枚举、注解），ElementType.FIELD，ElementType.METHOD
* @Inject：ElementType.CONSTRUCTOR，ElementType.METHOD，ElementType.FIELD
## 3. 装配类型
* @Autowired：默认是根据类型（byType）进行自动装配，如果有多个类型一样的Bean候选者时，则默认根据设定的属性名称（byName）进行获取，如果要获取限定其中一个候选者，则需要结合@Qualifier注解注解使用
* @Resource：默认是根据属性名称（byName）进行自动装配的，如果有多个类型一样的Bean候选者，则可以通过name指定进行注入，name的作用相当于@Qualifier注解；可以通过type属性，转为根据类型装配；如果byName匹配不到，就通过byType匹配，如果都匹配不到，就抛出异常
* @Inject：默认是根据类型（byType）进行自动装配，也可以结合@Named注解使用，改为根据名称（byName）装配
## 4. 比较
* @Autowired与@Inject
   相同点：用法基本一样，都是默认根据类型进行装配，都可以结合其他注解（@Autowired结合@Qualifier、@Inject结合@Named）转为根据名称进行装配
   不同点：@Autowired是Spring框架自带注解，@Inject是通过JSR330规范实现的，在javax.inject.Inject包下；@Inject注解缺少required属性，所以IOC Container中没有对应的Bean时，会抛出NoSuchBeanDefinitionException异常； 
* @Autowired与@Resource
   不同点：@Autowired是Spring框架自带注解，@Resource是通过JSR250规范实现的，在javax.annotaion包下；@Autowired默认根据类型自动装配，@Resource默认根据名称自动装配；存在多个同类型Bean候选者情况下，@AutoWired结合@Qualifier使用，可以转为根据名称装配，而@Resource通过name属性进行指定，且无法转为根据类型自动装配；
* @Resource与@Inject
   不同点：@Resource是通过JSR250规范实现的，在javax.annotation包下，@Inject是通过JSR330规范实现的，在javax.inject.Inject包下；@Resource默认根据名称进行自动装配，存在多个同类型Bean候选者情况下，可以通过name属性指定，@Inject默认根据类型进行自动装配，存在多个同类型Bean候选者情况下，可以结合@Named注解指定Bean，转为根据名称进行装配