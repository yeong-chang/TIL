# MyBatis 환경설정 

## pom 추가
```xml
<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.16</version>
</dependency>
        <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
<dependency>
<groupId>org.mybatis</groupId>
<artifactId>mybatis-spring</artifactId>
<version>2.1.2</version>
</dependency>
```

## MyBatis 설정 파일

### mybatis-config.xml
- 파일 위치 <mark>src/main/resources/mybatis-config.xml</mark>  
![mybatis-config_xml.png](img%2Fmybatis-config_xml.png)
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
  PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-config.dtd">
       

<configuration>
    
    <!-- SqlSessionTemplate 설정 -->
    <settings>
        <setting name="logImpl" value="LOG4J2"/>
    </settings>
    
    <!-- Java 클래스 별칭 작성 부분 -->
    <typeAliases>
    <typeAlias type="com.pcwk.ehr.board" alias="board"/>
    </typeAliases>

    <!-- SQL이 작성되는 mapper 파일 위치 등록 -->
    <mappers>
        <!-- 
            <mapper resource=""/>의 작성 기준
            ->src/main/resources 폴더
         -->
        <mapper resource="/mapper/board/board-mapper.xml"/>
    </mappers>
</configuration>
```
### boardMapper.xml
- 파일 위치는 mybatis-config.xml에서 설정 한 것처럼
  <mark>src/main/resource/mapper/board/board-mapper.xml</mark>  
![boardmapperxml위치.png](img%2Fboardmapperxml%EC%9C%84%EC%B9%98.png)
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  "https://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="com.pcwk.ehr.mapper.BoardMapper">
  <select id="selectBoard" resultType="BoardVO">
    select * from Board
  </select>
</mapper>
```

### log4j2.properties
<mark>src/main/resource/log4j2.properties</mark>
```properties
logger.mybatis.name = org.apache.ibatis
logger.mybatis.level = DEBUG
logger.mybatis.additivity = false
logger.mybatis.appenderRefs = stdout, rolling
logger.mybatis.appenderRef.stdout.ref = STDOUT
logger.mybatis.appenderRef.rolling.ref = roll
```