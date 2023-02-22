# 터미널에서 DB 접속정보 암/복호화 하는방법 
> url : https://hyeounstory.tistory.com/108
> - jasypt 라이브러리에서 제공해주는 StandardPBEStringEncryptor 방식으로 암복호화 한다고 생각하면 된다.
>> 1. 암호화할때는 test로직(java소스) 통해서 암호화되고,
>> 2. 복호화할때는 context-common.xml의 빈을 스프링이 자체적으로 읽어 jdbc.properties값 복호화하고, DB 연결한다고 생각하면 된다.

# Spring에서 DB 접속정보 암/복호화 하는방법 

1. context-common.xml에 DB연결을 위한 설정값 적용

```java
<bean id="encryptorConfig" class="org.jasypt.encryption.pbe.config.EnvironmentStringPBEConfig">
	<property name="algorithm" value="PBEWithMD5AndDES" />
	<property name="passwordEnvName" value="APP_ENCRYPTION_PASSWORD" />
</bean>
   
<bean id="encryptor" class="org.jasypt.encryption.pbe.StandardPBEStringEncryptor">
	<property name="config" ref="encryptorConfig" />
	<property name="password" value="tm-----vha" />
</bean>
```

2. jasypt를 활용하여 암복호화하는 테스트 로직

```java
@Test
public void test() {
	StandardPBEStringEncryptor pbeEnc = new StandardPBEStringEncryptor();
	pbeEnc.setPassword("tm-----vha"); // PBE 값 (XML PASSWORD설정)

    System.out.println("암호화 url : " + pbeEnc.encrypt("jdbc:log4jdbc:postgresql://10.***.***.***:5432/postgres?currentSchema=fin_common&autosave=conservative"));
    System.out.println("암호화 username : " + pbeEnc.encrypt("service"));
    System.out.println("암호화 password : " + pbeEnc.encrypt("app12$"));

    System.out.println("복호화 url : " + pbeEnc.decrypt("2Qu3ElBZPKGnR4sh5sjRBXcxLpg4VL-----SD/73ec59HrlK8kLStn1/2Y5C03SCx0o3"));
    System.out.println("복호화 username : " + pbeEnc.decrypt("ztskMXUQI-----XOPJkXURR"));
    System.out.println("복호화 password : " + pbeEnc.decrypt("eBtPzsXzk-----tu2VRnvTCdC"));

}
```

3. jdbc.properties에 접속정보 추가

```java
jdbc.finance.driver=net.sf.log4jdbc.DriverSpy
jdbc.finance.url=ENC(P6S67nHzYE/RehaxPJwzlab0/KKEzlQbdKaHCNKCfSvwFxsz0IOTkT7bCUZR+TZjudzMuhpEXR/+0A3j1ZhB19hBa1ydMp+Ms4NfFYp2DIaXRHC/UCdjqQ==)
jdbc.finance.username=ENC(GwuTdw6O8ntJvVHKTwp+1VGkQNPm2rvU)
jdbc.finance.password=ENC(GEmkjH+IKYKfo0TRtl/6oUPjqQQm7mrb)
```

3. context-datasource.xml에 DB 접속 빈 설정
