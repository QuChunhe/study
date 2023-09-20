

gradle

./gradlew Dependencies

# Configuration

[Commons Configuration](https://commons.apache.org/proper/commons-configuration/userguide/user_guide.html)


# Command-Line Interfaces

[Apache Commons CLI](https://commons.apache.org/proper/commons-cli/usage.html)


[shadow](https://imperceptiblethoughts.com/shadow/introduction/#benefits-of-shadow)


# assert 

```java
  assert x >= 0 : "x must >= 0";
```
要执行assert语句，必须给Java虚拟机传递-enableassertions（可简写为-ea）参数启用断言

也可以使用-da(Disabling Assertions)选项使断言无效（默认为无效）

# Junit

Unit Testing and Integration Testing

1. given
2. when
3. then

JUnit 5 = JUnit Platform + JUnit Jupiter + JUnit Vintage
> @Test
> @ParameterizedTest
> @RepeatedTest
> @TestFactory
> @TestTemplate
> @TestClassOrder
> @TestMethodOrder
> @TestInstance
> @DisplayName
> @DisplayNameGeneration
> @BeforeEach
> @AfterEach
> @BeforeAll
> @AfterAll
> @Nested
> @Tag
> @Disabled
> @Timeout
> @ExtendWith
> @RegisterExtension
> @TempDir


> org.junit.platform.launcher.core.LauncherFactory
> org.junit.platform.launcher.Launcher
> org.junit.platform.launcher.LauncherDiscoveryRequest
> org.junit.platform.launcher.TestPlan
> org.junit.platform.launcher.TestExecutionListener
> org.junit.platform.launcher.core.LauncherFactory
> org.junit.platform.engine.TestEngine

# Mockito

[Mockito](https://site.mockito.org/)

> @Mock, @Captor, @Spy  @InjectMocks


# AssertJ

[AssertJ Doc](https://assertj.github.io/doc/)

# JavaCC

JavaCC全称为Java Compiler Compiler，它是一个生成器，用于生成词法分析器（lexical analysers）和语法分析器（parsers）。

