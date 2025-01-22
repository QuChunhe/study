

gradle

./gradlew Dependencies

# Configuration

[Commons Configuration](https://commons.apache.org/proper/commons-configuration/userguide/user_guide.html)

# 性能分析工具

开源 Java 性能分析器比较：VisualVM、JMC 和 async-profiler


JDK Flight Recorder（JFR）


```shell
jcmd PID ManagementAgent.start \

    jmxremote.authenticate=false \

    jmxremote.ssl=false \

    jmxremote.port=5555

#加上以下的这两个参数即可开启对应的JFR功能
java -XX:+UnlockCommercialFeatures -XX:+FlightRecorder

#解锁JFR记录功能权限
java -XX:StartFlightRecording=disk=true,dumponexit=true,filename=recording.jfr,maxsize=1024m,maxage=1d,settings=profile,path-to-gc-roots=true test.Main

jcmd process_id JFR.start duration=10s filename=flight.jfr 
```

[深度探索JFR - JFR详细介绍与生产问题定位落地 - 1. JFR说明与启动配置](https://zhuanlan.zhihu.com/p/122247741)
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



ASN.1（Abstract Syntax Notation One) 是 ISO 和 ITU-T 的联合标准，是描述数据的表示、编码、传输、解码的灵活的记法。它提供了一套正式、无歧义和精确的规则以描述独立于特定计算机硬件的对象结构。


PKCS 协议组和 X.509 协议均采用 ASN.1 来定义密钥或证书的数据结构。


常见证书后缀

作为文件形式存在的证书一般有这几种后缀：(证书中包含公钥，以及公钥颁发机构、版本号、算法等信息，可以以X.509为例看一下证书内容)

1.带有私钥的证书：（一般都有密码保护，使用的是DER编码）
* .pfx 常用于Windows上的 IIS服务器
* .p12 常用于MAC OS、iOS中(PKCS#12由PFX进化而来的用于交换公共的和私有的对象的标准格式)
* .jks Java Key Storage，这是Java的专利，JAVA的专属格式，一般用于 Tomcat 服务器。

2.不带私钥的证书：
* .cer/crt 编码方式不一定，可能是DER也可能是PEM
* .pem 都是PEM编码格式
* .der 都是DER编码格式
* .p7b 以树状展示证书链(certificate chain)，同时也支持单个证书，不含私钥

3.补充
* .der文件一般只放证书，不含私钥
* .pem文件中可以放证书或者私钥，或者两者都有，pem如果只含私钥的话，一般用.key扩展名，而且可以有密码保护
* .csr - Certificate Signing Request，即证书签名请求，这个并不是证书，而是向权威证书颁发机构获得签名证书的申请，其核心内容是一个公钥(当然还附带了一些别的信息)，在生成这个申请的时候，同时也会生成一个私钥key，私钥要自己保管好。


Privacy-Enhanced Mail (PEM) 


PKCS stands for "Public Key Cryptography Standards"



DSA全称Digital Signature Algorithm，DSA只是一种算法，和RSA不同之处在于它不能用作加密和解密，也不能进行密钥交换，只用于签名，所以它比RSA要快很多，其安全性与RSA相比差不多。


ECDSA是用于数字签名，是ECC与DSA的结合，整个签名过程与DSA类似，所不一样的是签名中采取的算法为ECC，最后签名出来的值也是分为r,s。而ECC（全称Elliptic Curves Cryptography）是一种椭圆曲线密码编码学。


PKI（Public Key Infrastructure，公钥基础设施）是一种安全框架，用于创建、管理、分发、使用、存储和撤销数字证书。PKI建立了一种基于公钥加密的可信任关系，使得实体（如用户、组织或设备）能够相互验证和加密通信。PKI中的核心组件包括：
* 证书颁发机构（CA，Certificate Authority）：负责颁发、签署和撤销数字证书。
* 证书（Certificate）：包含实体的公钥、实体标识符、颁发者信息等，由CA数字签名。
* 证书库（Certificate Store）：存储和管理证书。
* 密钥对（Key Pair）：由公钥和私钥组成，用于加密和解密信


推荐使用的算法
* 256 位的 AES 算法
* SHA-256、SHA-512 单向散列函数
* RSASSA-PSS 签名算法
* X25519/X448 密钥交换算法
* EdDSA 签名算法



RSA（Rivest–Shamir–Adleman）是最早的公钥密码系统之一，被广泛用于安全数据传输。它的安全性取决于整数分解，因此永远不需要安全的RNG（随机数生成器）。与DSA相比，RSA的签名验证速度更快，但生成速度较慢。

DSA（数字签名算法）是用于数字签名的联邦信息处理标准。它的安全性取决于离散的对数问题。与RSA相比，DSA的签名生成速度更快，但验证速度较慢。如果使用错误的数字生成器，可能会破坏安全性。

ECDSA（椭圆曲线数字签名算法）是DSA（数字签名算法）的椭圆曲线实现。椭圆曲线密码术能够以较小的密钥提供与RSA相对相同的安全级别。它还具有DSA对不良RNG敏感的缺点。

EdDSA（爱德华兹曲线数字签名算法）是一种使用基于扭曲爱德华兹曲线的Schnorr签名变体的数字签名方案。签名创建在EdDSA中是确定性的，其安全性是基于某些离散对数问题的难处理性，因此它比DSA和ECDSA更安全，后者要求每个签名都具有高质量的随机性。

Ed25519是EdDSA签名方案，但使用SHA-512 / 256和Curve25519；它是一条安全的椭圆形曲线，比DSA，ECDSA和EdDSA 提供更好的安全性，并且具有更好的性能（人为注意）。

JCA与其他加密库的对比
1. Bouncy Castle

Bouncy Castle是一个流行的开源加密库，提供了许多Java未提供的加密算法。它可以作为JCA的一个提供者使用，但在某些场景下，Bouncy Castle的性能可能不如Java的内置加密库。

2. OpenSSL

OpenSSL是一个广泛使用的开源加密库，它主要针对C和C++应用程序。尽管可以在Java项目中使用JNI（Java Native Interface）调用OpenSSL，但与JCA相比，集成和使用相对更复杂。

3. LibreSSL

LibreSSL是一个OpenSSL的分支，致力于提供更安全和稳定的加密实现。与OpenSSL类似，它也主要针对C和C++应用程序，使用JNI调用的方式与Java集成。


* CN : Common Name 通用名，对于 SSL 证书，一般为网站域名；而对于代码签名证书则为申请单位名称；而对于客户端证书则为证书申请者的姓名；
* OU: organizationUnit 组织部门名
* O: Organization Name 组织名 对于 SSL 证书，一般为网站域名；而对于代码签名证书则为申请单位名称；而对于客户端单位证书则为证书申请者所在单位名称；
* L: Locality 城市
* S: State/Provice  省份
* C: country 只能是国家字母缩写，如中国：CN 


.ed25519_oid

secp256k1

"Ed25519"
RSA



证书的签发过程
1. 服务端向第三方 CA 机构提交公钥、组织信息、个人信息等信息并申请认证；
2. CA 通过线上、线下等多种手段验证申请者提供信息的真实性，如：组织是否存在、企业是否合法，是否拥有域名的所有权等；
3. 信息审核通过，CA 会向申请者签发认证文件 — 证书。证书包含以下信息：申请者公钥、申请者的组织信息和个人信息、签发机构 CA 的信息、有效时间、证书序列号等信息的明文，同时包含一个签名；CA 使用散列函数计算公开的明文信息的信息摘要，然后，采用 CA 的私钥对信息摘要进行加密，密文即 “签名”；
4. 客户端向服务端发出请求时，服务端响应证书文件给客户端；
5. 客户端读取证书中的相关的明文信息，采用相同的散列函数计算得到信息摘要，然后，利用对应 CA 的公钥解密签名数据，对比证书的信息摘要，如果一致，则可以确认证书的合法性，即公钥合法；
6. 客户端然后验证证书相关的域名信息、有效时间等信息；
7. 客户端会内置信任 CA 的证书信息（包含公钥），如果 CA 不被信任，则找不到对应 CA 的证书，证书也会被判定非法。
>> 证书 = 公钥 + 申请者与颁发者信息 + 签名


keytool，openssl 可以生成自签名证书
```
ssh
chcp 936
生成证书文件
keytool -genkeypair -alias ofd_server_cert  -keyalg EC -validity 3650 -keystore ofd_server.p12 -storetype pkcs12 -dname CN=北京仁和汇智信息技术有限公司,O=北京仁和汇智信息技术有限公司,L=北京,C=CN -storepass quchunhe

keytool -genkey -alias ofd_server_cert  -keyalg EC -validity 3650 -keystore ofd_server.p12 -storetype pkcs12 -dname CN=北京仁和汇智信息技术有限公司,O=北京仁和汇智信息技术有限公司,L=北京,C=CN -storepass quchunhe

查看证书
keytool -list -v -keystore ofd_server.p12 -storetype pkcs12 -storepass quchunhe

生成cer文件
keytool -export -alias ofd_server_cert -keystore ofd_server.p12 -storetype pkcs12  -storepass quchunhe -file ofd_server.cer

提取私钥



keytool -certreq -alias golove -keystore teststore.jks -file temp_go_love.csr

keytool -certreq -keyalg  EC -keysize 512
```
https://www.chinassl.net/ssltools/keytool-commands.html


格式
* .der或*.cer文件： 这样的证书文件是二进制格式，只含有证书信息，不包含私钥。
* .crt文件： 这样的证书文件可以是二进制格式，也可以是文本格式，一般均为文本格式，功能与 *.DER及*.CER证书文件相同。
* .pem文件： 这样的证书文件一般是文本格式，可以存放证书或私钥，或者两者都包含。 *.PEM 文件如果只包含私钥，一般用*.KEY文件代替。
* .pfx或*.p12文件： 这样的证书文件是二进制格式，同时包含证书和私钥，且一般有密码保护。
* .JKS，二进制格式，同时包含证书和私钥，一般有密码保护。