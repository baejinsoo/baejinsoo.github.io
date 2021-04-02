---
title: "Web Service, soap vs rest"
excerpt: "Spring Boot를 이용한 RESTful Web Services 개발"
categories:
  - Spring
last_modified_at: 2021-04-02
toc: trues
toc_sticky: true
---

## Web Service와 Web Application

### Web Service

![image-20210402211946911](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210402211946911.png)

World Wide Web 를 통한 device와 device간의 통신 서비스

네트워크 상에서 특정한 포트를 열어 놓은 서버가 클라이언트 요청을 받은 다음 웹 문서(HTML, JSON, XML, images)를 제공하는 것, HTTP 를 통해 특정한 도메인의 문제를 해결하기 위한 서비스

👉 네트워크 상에서 서로 다른 종류의 컴퓨터들 간에 상호작용하기 위한 소프트웨어 시스템



### Web Application

서버에 저장되어있고 Web browser를 통해서 실행할 수 있는 프로그램



### Web Service

![image](https://user-images.githubusercontent.com/17541671/113416944-519a2e80-93fd-11eb-8763-106e84f312ee.png)



#### Soap (Simple Object Access Protocol)

> HTTP, HTTPS, SMTP 등을 사용하여 XML 기반의 메시지를 컴퓨터 네트워크 상에서 교환하는 형태의 프로토콜

![image](https://user-images.githubusercontent.com/17541671/113417337-23691e80-93fe-11eb-922c-f929fa8bb652.png)

- tag로 감싸주어야 한다. => 복잡한 구조(오버헤드가 심하다.), 무겁다

#### RESTful (Representational State Transfer)

> 네트워크 아키텍처 원리의 모음 => 자원을 정의하고 자원에 대한 주소를 지정하는 전반적인 방법
>
> Reource의  Representation에 의한 상태 전달
>
> HTTP Method를 통해 Resource를 처리하기 위한 아키텍처

![image-20210402220311713](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210402220311713.png)

### Reference

> <https://en.wikipedia.org/wiki/Web_service>
>
> <https://en.wikipedia.org/wiki/Web_application>
>
> <https://en.wikipedia.org/wiki/Representational_state_transfer>
>
> <http://blog.wishket.com/soap-api-vs-rest-api-%EB%91%90-%EB%B0%A9%EC%8B%9D%EC%9D%98-%EA%B0%80%EC%9E%A5-%ED%81%B0-%EC%B0%A8%EC%9D%B4%EC%A0%90%EC%9D%80/>
>
> <https://www.inflearn.com/course/spring-boot-restful-web-services>

