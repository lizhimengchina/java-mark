## JUnit单元测试--IntelliJ IDEA

### 单元测试的基本使用

一、环境配置

​     使用idea IDE 进行单元测试，首先需要安装JUnit 插件。

​          1.安装JUnit插件步骤

​              File-->settings-->Plguins-->Browse repositories-->输入JUnit-->选择JUnit Generator V2.0安装。

​          2.使用JUnit插件

​             在需要进行单元测试的类中，使用快捷键alt+insert，选择JUnit test，选择JUnit4。

二、单元测试

代码Demo：

```java
　@Test
    public void testAdd() {
        assertEquals(2, new UserDao().add(1, 1));
    }
```

1>注意事项：

　　　　1、测试方法上面必须使用@Test注解进行修饰。

　　　　2、测试方法必须使用public void 进行修饰，不能带有任何参数。

　　　　3、新建一个源代码目录用来存放测试代码。

　　　　4、测试类的包应该与被测试类的包保持一致。

　　　　5、测试单元中的每一个方法必须独立测试，每个测试方法之间不能有依赖。

　　　　6、测试类使用Test做为类名的后缀（非必要）。

　　　　7、测试方法使用test作为方法名的前缀（非必要）。

2>错误解析：

　　　　1、Failure 一般是单元测试使用的断言方法判断失败引起，说明预期结果和程序运行结果不一致。

　　　　2、error 是有代码异常引起的，他产生于测试代码本身中的Bug。

　　　　3、测试用例是不是用来证明你是对的，而是用来证明你没有错。

3>测试流程：

代码Demo： 

```
@BeforeClass
    public static void setUpBeforeClass() throws Exception {

    }
    @AfterClass
    public static void setUpAfterClass() throws Exception {

    }

    @Before
    public void before() throws Exception {

    }

    @After
    public void after() throws Exception {

    }
```

　1、@BeforeClass所修饰的方法在所有方法加载前执行，而且他是静态的在类加载后就会执行该方法，

　　　　　　　  在内存中只有一份实例，适合用来加载配置文件。

　　　　　　2、@AfterClass所修饰的方法在所有方法执行完毕之后执行，通常用来进行资源清理，例如关闭数据库连接。

　　　　　　3、@Before和@After在每个测试方法执行前都会执行一次。

4>常用注解

　　　　　　1、@Test(excepted=XX.class) 在运行时忽略某个异常。

　　　　　　2、@Test(timeout=毫秒) 允许程序运行的时间。

　　　　　　3、@Ignore 所修饰的方法被测试器忽略。

　　　　　　4、RunWith 可以修改测试运行器 org.junit.runner.Runner

5>测试套件

　　　　 　测试套件是组织测试类一起运行的测试类。具体如下：

代码Demo：

```java
@RunWith(Suite.class)
@Suite.SuiteClasses({UserTest1,UserTest2,UserTest3})
public class SuiteTest{
    
}
```

注意事项：

　　　　　　1、作为测试套件的入口类，类中不能包含任何方法。

　　　　　　2、更改测试运行器Suite.class。

　　　　　　3、将需要运行的测试类放入Suite.SuiteClasses({})的数组中。

6>参数化设置

　　　　　　需要测试的仅仅是测试数据，代码结构是不变的，只需要更改测试数据。

代码Demo：　　　　

```
@RunWith(Parameterized.class)
public class parameterTest {
    int expected = 0;
    int input1 = 0;
    int input2 = 0;

    @Parameters
    public static Collection<Object[]> t() {
        return Arrays.asList(new Object[][]{
                {3,1,2},
                {5,2,3}
        });
    }

    public parameterTest(int expected,int input1,int input2) {
        this.expected = expected;
        this.input1 = input1;
        this.input2 = input2;
    }

    @Test
    public void testAdd() {
        assertEquals(expected, UserDao.add(input1,input2));
    }

}
```

具体步骤：

　　　　　　　　1、更改默认的测试运行器为@RunWith(Parameterized.class)。

　　　　　　　　2、声明变量来存放预期值和测试值。

　　　　　　　　3、声明一个返回值为Collection的公共静态方法，并用@Parameters修饰。

　　　　　　　　4、为测试类声明一个带有参数的公共构造函数，并在其中为他声明变量赋值。

以上为基于IntelliJ IDEA 进行的单元测试。　　　