# 단방향 암호화
단방향 암호화: 암호화된 암호문을 복호화 불가능한 암호화

Spring Security에서 단방향 암호화는 주로 PasswordEncoder인터페이스와 BCryptPassowrdEncoder구현체를 사용 합니다.

---

## 주요 특징
- 해싱(Hashing) : 복호화할 수 없는 비밀번호 저장방식.
- BCrypt알고리즘: Salt를 포함하여 해시를 생성하므로 동일한 입력값도 다른 해시값을 생성.


## pom에 SpringSecurity dependency추가
```xml
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-core</artifactId>
    <version>5.8.13</version>
</dependency>


<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-web</artifactId>
    <version>5.8.13</version>
</dependency>


<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-config</artifactId>
    <version>5.8.13</version>
</dependency>
```

## root-context.xml에 bean추가
```xml
<!-- 단방향 암호화 -->
    <bean id="passwordEncoder" 
    class="org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder">
    </bean>
```


