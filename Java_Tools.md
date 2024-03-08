

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

# Java Cryptography Architecture (JCA)

[Java加密体系（JCA](https://www.xuanyuanli.cn/pages/5c445e/)

消息摘要（Message Digest）消息摘要可以用于验证数据完整性

数字签名（Digital Signature）

 对称加密（Symmetric Encryption）

非对称加密（Asymmetric Encryption）

密钥交换（Key Exchange）

密钥存储（KeyStore）


公钥基础设施(Public Key Infrastructure, PKI)是典型的密码应用技术。在 PKI 系统中， 由证书认证机构(Certification Authority, CA)签发数字证书、绑定 PKI 用户的身份信息和公钥。 PKI 依赖方(Relying Party)预先存储有自己所信任的根 CA 自签名证书,，用来验证与之通信的 PKI 用户的证书链,，从而可信地获得该用户的公钥、用于各种安全服务。

1978 年， L. Kohnfelder 首次提出证书的概念；1988 年，第一版本的 X.509 标准推出，发展至 2005 年的版本 3 标准；1995 年，IETF 成立 PKIX 工作组，将 X.509 标准用于 Internet， 2013 年,，IETF PKIX 工作组结束工作任务。