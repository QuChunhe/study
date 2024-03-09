

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


对称加密AES，非对称加密: ECC，消息摘要: MD5，数字签名:DSA

消息摘要（Message Digest）消息摘要可以用于验证数据完整性

数字签名（Digital Signature）

 对称加密（Symmetric Encryption）

非对称加密（Asymmetric Encryption）

密钥交换（Key Exchange）

密钥存储（KeyStore）


公钥基础设施(Public Key Infrastructure, PKI)是典型的密码应用技术。在 PKI 系统中， 由证书认证机构(Certification Authority, CA)签发数字证书、绑定 PKI 用户的身份信息和公钥。 PKI 依赖方(Relying Party)预先存储有自己所信任的根 CA 自签名证书,，用来验证与之通信的 PKI 用户的证书链,，从而可信地获得该用户的公钥、用于各种安全服务。

RSA由Ron Rivest，Adi Shamir和Leonard Adleman（因此称为“RSA”）于1977年发明，是迄今为止使用最广泛的非对称加密算法

1978 年， L. Kohnfelder 首次提出证书的概念；1988 年，第一版本的 X.509 标准推出，发展至 2005 年的版本 3 标准；1995 年，IETF 成立 PKIX 工作组，将 X.509 标准用于 Internet， 2013 年,，IETF PKIX 工作组结束工作任务。

1985年，两位名叫Neal Koblitz和Victor S. Miller的数学家提议在密码学中使用椭圆曲线。近二十年后，当ECC（椭圆曲线密码学）算法于2004-05年投入使用。

[Java Security Standard Algorithm Names](https://docs.oracle.com/en/java/javase/17/docs/specs/security/standard-names.html)

一套 数字签名 通常定义两种 互补 的运算，一个用于 签名，另一个用于 验证。分别由 发送者 持有能够 代表自己身份 的 私钥 (私钥不可泄露),由 接受者 持有与私钥对应的 公钥 ，能够在 接受 到来自发送者信息时用于 验证 其身份。

MD5算法
MD5 用的是 哈希函数，它的典型应用是对一段信息产生 信息摘要，以 防止被篡改。严格来说，MD5 不是一种 加密算法 而是 摘要算法。无论是多长的输入，MD5 都会输出长度为 128bits 的一个串 (通常用 16 进制 表示为 32 个字符)。

SHA1算法

SHA1 是和 MD5 一样流行的 消息摘要算法，然而 SHA1 比 MD5 的 安全性更强。对于长度小于 2 ^ 64 位的消息，SHA1 会产生一个 160 位的 消息摘要。


```java
import java.security.MessageDigest;
import java.util.Arrays;

public class MessageDigestExample {
    public static void main(String[] args) throws Exception {
        String message = "Hello, JCA!";
        MessageDigest md = MessageDigest.getInstance("SHA-256");
        byte[] digest = md.digest(message.getBytes());
        System.out.println("Message Digest: " + Base64.getEncoder().encodeToString(digest));
    }
}
```


HMAC 是密钥相关的 哈希运算消息认证码（Hash-based Message Authentication Code），HMAC 运算利用 哈希算法 (MD5、SHA1 等)，以 一个密钥 和 一个消息 为输入，生成一个 消息摘要 作为 输出。

HMAC 发送方 和 接收方 都有的 key 进行计算，而没有这把 key 的第三方，则是 无法计算 出正确的 散列值的，这样就可以 防止数据被篡改。

MAC算法可选以下多种算法： HmacMD5/HmacSHA1/HmacSHA256/HmacSHA384/HmacSHA512


```java
import java.security.*;
import java.util.Base64;

public class DigitalSignatureExample {
    public static void main(String[] args) throws Exception {
        String message = "Hello, JCA!";
        
        KeyPairGenerator keyPairGenerator = KeyPairGenerator.getInstance("RSA");
        KeyPair keyPair = keyPairGenerator.generateKeyPair();
        PublicKey publicKey = keyPair.getPublic();
        PrivateKey privateKey = keyPair.getPrivate();

        // 使用私钥进行加密
        Signature signature = Signature.getInstance("SHA256withRSA");
        signature.initSign(privateKey);
        signature.update(message.getBytes());
        byte[] signedData = signature.sign();
        String encodedSignedData = Base64.getEncoder().encodeToString(signedData);
        System.out.println("Signed Data: " + encodedSignedData);

        // 使用公钥进行验证
        Signature verifySignature = Signature.getInstance("SHA256withRSA");
        verifySignature.initVerify(publicKey);
        verifySignature.update(message.getBytes());
        boolean isVerified = verifySignature.verify(signedData);
        System.out.println("Signature verification: " + isVerified);
    }
}

```