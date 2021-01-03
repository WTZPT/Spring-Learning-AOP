# 工程简介
对Spring AOP进行练习

# 注解总结
### @Pointcut
@Pointcut 注解，用来定义一个切面，即上文中所关注的某件事情的入口，切入点定义了事件触发时机

### @Around
@Around注解用于增强处理，表现在：

- @Around可以自由选择增强动作与目标方法的执行顺序，也就是说可以在增强动作前后，甚至过程中执行目标方法。这个特性的实现在于，调用ProceedingJoinPoint参数的procedd()方法才会执行目标方法。

- @Around可以改变执行目标方法的参数值，也可以改变执行目标方法之后的返回值。

@Around增强处理有以下特点：

- 当定义一个Around增强处理方法时，该方法的第一个形参必须是 ProceedingJoinPoint 类型（至少一个形参）。在增强处理方法体内，调用ProceedingJoinPoint的proceed方法才会执行目标方法：这就是@Around增强处理可以完全控制目标方法执行时机、如何执行的关键；如果程序没有调用ProceedingJoinPoint的proceed方法，则目标方法不会执行。

- 调用ProceedingJoinPoint的proceed方法时，还可以传入一个Object[ ]对象，该数组中的值将被传入目标方法作为实参——这就是Around增强处理方法可以改变目标方法参数值的关键。这就是如果传入的Object[ ]数组长度与目标方法所需要的参数个数不相等，或者Object[ ]数组元素与目标方法所需参数的类型不匹配，程序就会出现异常。

- @Around功能虽然强大，但通常需要在线程安全的环境下使用。因此，如果使用普通的Before、AfterReturning就能解决的问题，就没有必要使用Around了。如果需要目标方法执行之前和之后共享某种状态数据，则应该考虑使用Around。尤其是需要使用增强处理阻止目标的执行，或需要改变目标方法的返回值时，则只能使用Around增强处理了。

### @Before / @After
  @Before指定的方法在切面切入目标方法之前执行， @After与之相对应，指定的方法在切面切入目标方法之后执行,它们可以做一些 Log 处理，也可以做一些信息的统计
 
### @AfterReturning
@AfterReturning 注解和 @After 有些类似，区别在于 @AfterReturning 注解可以用来捕获切入方法执行完之后的返回值，对返回值进行业务逻辑上的增强处理

###  @AfterThrowing
当被切方法执行过程中抛出异常时，会进入 @AfterThrowing 注解的方法中执行，在该方法中可以做一些异常的处理逻辑。要注意的是 throwing 属性的值必须要和参数一致，否则会报错。该方法中的第二个入参即为抛出的异常
