---
layout: single
title: "Java와 MySQL을 JDBC로 연결하기"
categories: MySQL
tag: [MySQL, JAVA]
toc: true
author_profile: false
sidebar:
    nav: "docs"
search: true
---

> java에서 mysql 데이터베이스에 접근, 조작을 위해 연결하기   
> JDBC API를 통해 데이터 베이스에 연결함.

## JDBC란? 
java database connectivity, 데이터베이스와 상호작용할 수 있게 해주는 표준 API    

## Java와 MySQL 연결하기   
MySQL과 eclipse 환경에서의 java가 깔려있다는 전제하에 작성하였음.   
### JDBC 드라이버 다운로드
[MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/)
에 들어가 다운로드 하기   

이 때, window 기반 환경에서는 Platform Independent 선택 후 zip 파일 형태를 다운로드 한다.   
![image](https://github.com/user-attachments/assets/9a439467-c9eb-407b-8534-5ac56856c469)

다운로드 후 압축을 풀고 파일에 들어가면 jar 파일이 존재하는데, 이 파일을 사용하여 연결한다.   

![image](https://github.com/user-attachments/assets/08646726-7119-4b27-ad09-cfe2d4247cc3)

## java에 JDBC 드라이버 설정하기
java 프로젝트에 우클릭 후 Build Path - Configure Build Path...에 들어간다.   

![image](https://github.com/user-attachments/assets/45a3b4f4-c5bb-4080-a867-92ae1ca92ea5)

그 후 Libraries로 이동 후, Classpth에 Add External JARs..를 클릭한다.   
![image](https://github.com/user-attachments/assets/0dfa8183-cfa9-4556-af8e-37adce9b3412)

클릭 후 아까 저장해 둔 파일에서 jar 파일을 선택한다.    
이 후, Apply and close   
![image](https://github.com/user-attachments/assets/beb8d463-15eb-4401-b99b-a5ded4648356)

그러면, 해당 프로젝트에 Referenced Libraries가 새로 생긴 것을 확인할 수 있다.   
![image](https://github.com/user-attachments/assets/a03b426b-982f-469d-8593-580e0276355a)

이후 src패키지의 module-info.java파일을 다음과 같이 수정해준다.   
![image](https://github.com/user-attachments/assets/e6a0fced-15d8-4509-943a-a55bf92d7689)

## Java 코드로 MySQL 연결하기
MySQL의 mydb라는 이름의 데이터베이스에 연결하였음.   

새 파일을 생성하여 아래의 예시 코드를 통해 연결하였다.   
이 때, URL, USER name, PASSWORD를 각자 환경에 맞게 수정해야 한다.   

성공적으로 연결되어 ***MySQL 데이터베이스에 성공적으로 연결되었습니다.*** 가 출력된 것을 볼 수 있다.   

이제 try 문 안에 원하는 쿼리문을 넣어 출력할 수 있게 된다.   
![image](https://github.com/user-attachments/assets/f84091da-2616-47a1-a7e5-5f91a25b0a83)

```java
package mydb; // 패키지명 변경

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class JDBConnection {
    // 데이터베이스 URL, 사용자명, 비밀번호
    private static final String URL = "jdbc:mysql://localhost:3306/mydb"; // 사용자 URL
    private static final String USER = "root"; // 사용자명
    private static final String PASSWORD = "1234"; // 비밀번호

    public static void main(String[] args) {
        try (Connection conn = DriverManager.getConnection(URL, USER, PASSWORD)) {
            System.out.println("MySQL 데이터베이스에 성공적으로 연결되었습니다.");
        } catch (SQLException e) {
            System.out.println("데이터베이스 연결 실패");
            e.printStackTrace();
        }
    }
}

```