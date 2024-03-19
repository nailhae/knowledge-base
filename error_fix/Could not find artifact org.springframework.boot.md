Spring Boot를 공부하면서 jdbc 의존성을 추가했는데 에러가 발생했고, 해결한 과정을 소개합니다.

## 목차
- [개발환경](#개발환경)
- [추가한 의존성 내용](#추가한-의존성-내용)
- [발생한 에러](#발생한-에러)
- [시도한 방법](#시도한-방법)
- [최종 해결 방법](#최종-해결-방법)
- [소감 및 깨달은 점](#소감-및-깨달은-점)

## 개발환경
- M2 Air
- IntelliJ
- Maven

## 추가한 의존성 내용
```xml
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>springboot-starter-jdbc</artifactId>
		</dependency>
```

## 발생한 에러
```sh
Could not find artifact org.springframework.boot:springboot-starter-jdbc:pom:unknown in central (https://repo.maven.apache.org/maven2)
```

## 시도한 방법
- `Could not find artifact org.springframework.boot` 를 구글 검색. 대부분 글이 `.../m2/repository`를 삭제한 후 다시 의존성 파일을 설치하는 것이었는데 해결되지 않았다.

## 최종 해결 방법
- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-jdbc/3.2.3 주소에서 `Maven`에 해당하는 내용(아래)을 추가하고 IntelliJ에 생긴 의존성 새로고침 버튼(`Load Maven Changes`)을 누르니 해결되었다.
```xml
<!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-jdbc -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jdbc</artifactId>
    <version>3.2.3</version>
</dependency>
```

## 소감 및 깨달은 점
- 에러 원인은 https://repo.maven.apache.org/maven2 주소에서 jdbc 내용을 찾지 못한 것이었다. 의존성 repository를 지워도 해결되지 않는 것이 당연한 결과다.
- 검색 결과를 무턱대고 따라하지 않도록 해야겠다는 생각이 들었다. 그러나 당시에는 해결될 수도 있을 거라 생각해서 했던 시도.
- 해결된 방법에는 `version`정보가 추가된 것이 차이인데 https://repo.maven.apache.org/maven2 에는 jdbc 3.2.3은 없었다. 주석으로 처리된 주소에서 의존성 정보를 받아온 것일까?
