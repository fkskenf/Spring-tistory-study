# 터미널에서 DB 접속정보 암/복호화 하는방법 
> url : https://hyeounstory.tistory.com/108

# Spring에서 DB 접속정보 암/복호화 하는방법 

1. context-common.xml에 암복화화를 위한 password를 가진 빈 설정 

```java
<bean id="encryptorConfig" class="org.jasypt.encryption.pbe.config.EnvironmentStringPBEConfig">
	<property name="algorithm" value="PBEWithMD5AndDES" />
	<property name="passwordEnvName" value="APP_ENCRYPTION_PASSWORD" />
</bean>
   
<bean id="encryptor" class="org.jasypt.encryption.pbe.StandardPBEStringEncryptor">
	<property name="config" ref="encryptorConfig" />
	<property name="password" value="tmzkdlvmffotvha" />
</bean>
```

1. jdbc.properties에 접속정보 추가

```java
jdbc.finance.driver=net.sf.log4jdbc.DriverSpy
jdbc.finance.url=ENC(P6S67nHzYE/RehaxPJwzlab0/KKEzlQbdKaHCNKCfSvwFxsz0IOTkT7bCUZR+TZjudzMuhpEXR/+0A3j1ZhB19hBa1ydMp+Ms4NfFYp2DIaXRHC/UCdjqQ==)
jdbc.finance.username=ENC(GwuTdw6O8ntJvVHKTwp+1VGkQNPm2rvU)
jdbc.finance.password=ENC(GEmkjH+IKYKfo0TRtl/6oUPjqQQm7mrb)
```

- 추가) jasypt를 활용하여 암복호화 임의로 하는 테스트 로직

```java
@Test
	public void test() {
		StandardPBEStringEncryptor pbeEnc = new StandardPBEStringEncryptor();
		pbeEnc.setPassword("tmzkdlvmffotvha"); // PBE 값(XML PASSWORD설정)
		
	    String url = pbeEnc.encrypt("jdbc:log4jdbc:postgresql://10.70.165.64:5432/postgres?currentSchema=fin_common&autosave=conservative");
	    String username = pbeEnc.encrypt("service_app");
	    String password = pbeEnc.encrypt("DBP!app123$");
	 
	    System.out.println("암호화 url : " + url);
	    System.out.println("암호화 username : " + username);
	    System.out.println("암호화 password : " + password);
	    
	    System.out.println("복호화 url : " + pbeEnc.decrypt("2Qu3ElBZPKGnR4sh5sjRBXcxLpg4VLLCKycdJdsC/5d3y3mdiJx71VHWd1iKHdatSey0iCqqGoFMcR+ZUx5AgBRup07pRkSLetdYmj+WrFDeO6B3Un+BVWVM8LFT6WzSD/73ec59HrlK8kLStn1/2Y5C03SCx0o3"));
	    System.out.println("복호화 username : " + pbeEnc.decrypt("ztskMXUQI9ZZwEK13hqCS4QXOPJkXURR"));
	    System.out.println("복호화 password : " + pbeEnc.decrypt("eBtPzsXzkUVan79vquv6ntu2VRnvTCdC"));
		
	}
```
