# Maven

* Spring 프로젝트에 필요한 jar 파일을 코드로 쉽게 설치, 삭제 하도록 해줌

<br>

#### `pom.xml`

```
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>hello_di</groupId>
  <artifactId>hello_di</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  <build>
    <sourceDirectory>src</sourceDirectory>
    <plugins>
      <plugin>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.8.0</version>
        <configuration>
          <source>1.8</source>
          <target>1.8</target>
        </configuration>
      </plugin>
    </plugins>
  </build>
  <dependencies>
  	<!-- https://mvnrepository.com/artifact/org.springframework/spring-context -->
	<dependency>
     	<groupId>org.springframework</groupId>
    	<artifactId>spring-context</artifactId>
    	<version>5.3.9</version>
	</dependency>
  </dependencies>
</project>
```

* spring-context jar 파일 가져오는 코드 부분

  ```
  <dependencies>
    	<!-- https://mvnrepository.com/artifact/org.springframework/spring-context -->
  	<dependency>
       	<groupId>org.springframework</groupId>
      	<artifactId>spring-context</artifactId>
      	<version>5.3.9</version>
  	</dependency>
    </dependencies>
  ```

* 해당 코드 가져올 수 있는 사이트

  `https://mvnrepository.com/`