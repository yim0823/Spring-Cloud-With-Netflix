# Spring-Cloud-Netflix
Spring Cloud에 Netflix OSS(Open Source Software)를 사용할 수 있도록 한다. 즉, Microservice Architecture 구축에 필요한 여러 기능들을 Netflix OSS에서 
라이브러리로 제공하고 이를 Spring Cloud 프로젝트에서 사용할 수 있다.


Spring Cloud
----------------
- Microservice Architecture 구축을 위해 필요한 모든 라이브러리의 집합이다.
- Spring Cloud는 가장 보편화된 분산시스템 패턴에 대해서 단순하고 접근 가능한 프로그래밍 모델을 제공한다.
- 개발자가 복원성(resilient), 신뢰성(reliable), 조정된 어플리케이션(coordinated applications)을 구축할 수 있도록 지원한다.
- Spring Cloud는  '스프링 부트' 기반위에서 구성됨으로써 개발자가 쉽고 빠르게 만들 수 있고, 빠르게 생산성을 높일 수 있다.
- Tweleve-Factor APP이란 방법론을 기반으로 Software as a Service(SaaS)를 가능케한다.
 - 확장성(Scable)하게 클라우드 환경에서 플랫폼을 쉽게 배포할 수 있고 지속적인 배포(CI)가 가능하도록 한다.

<div>
<img src="https://user-images.githubusercontent.com/3222837/57754994-b3c6e900-772a-11e9-8c34-189be4056760.png">
</div>

Netflix OSS
----------------
Netflix의 MSA 노하우가 깃든 개념들을 Component화하여 오픈 소스 라이브러리로 제공한 것으로 Spring Cloud에 적용되어 MSA 구축을 손쉽게 할 수 있게 도와준다.
- 주요 기능 구성들

| Function | Solution | 
| ---------- | --------- | 
| Service Discovery Server | Netflix Eureka | 
| Central Configuration Server | Spring Cloud Configuration Server | 
| Dynamic Routing and Loadbalancer | Netflix Ribbon | 
| Circuit Breaker | Netflix Hystrix | 

- 지원 기능들

| Function | Solution | 
| ---------- | --------- | 
| Edge Server | Netflix Zuul | 
| OAuth 2.0 protected APIs | Spring-Cloud-Security | 
| Monitoring | Netflix Hystrix dashboard + Turbine | 
| Centralized Log Analysis | ELK (Elasticsearch + Logstash + Kibana) | 

- System Landscape
<div>
<img src="https://user-images.githubusercontent.com/3222837/57756430-31402880-772e-11e9-8b6b-95976e2c88c5.png">
</div>

Service discovery with Eureka
----------------
- Eureka는 Service Discovery & Registry 역할을 제공한다. 
- Service 단위로 시스템이 구축되다 보니 MSA에서는 이 Service들은 어떠한 Registry에 등록하고, 이 Registry를 기반으로 다른 서비스를 찾는 Service Discovery & Registry라는 개념이 필요하다.
   - Eureka는 크게 Eureka Server와 Eureka Client로 나뉘어 진다. Microsericie Architecture 시스템에서의 모든 service들은 Eureka Client로 만들어지게 된다. 그리고 Eureka Client(각 service)들은 자신을 Eureka Server(Registry)에 등록한다. Eureka Client는 자신을 Eureka Server에 등록하고 hostname, ip address, port 등 자신의 meta data를 Eureka Server(Registry)에 전송한다.
   - 이 meta data는 Eureka Server(Registry)에 저장되는 것이다. 그리고 등록된 Eureka Client는 이 Registry에 저장된 다른 Eureka Client의 정보를 사용할 수 있다. 

- Eureka Client인 경우에는 'spring-cloud-starter-eureka'를 등록해주어야 한다. Client는 항상 discovery server에 서비스를 등록할 책임이 있는데, 이 역할을 해주는 클래스가 해당 패키지에 있다. ( EurekaRegistration ) 
- Eureka Server인 경우에는 'spring-cloud-starter-eureka-server' 패키지를 포함하면 된다. 
<div>
<img width="500" src="https://user-images.githubusercontent.com/3222837/57757488-8b41ed80-7730-11e9-9dd6-c6f37cb23104.png">
<img width="300" src="https://user-images.githubusercontent.com/3222837/57757678-f7245600-7730-11e9-86b4-5263e6181205.png">
</div>

여기서는 Eureka란 무엇인지, 어떻게 구성되어있는지, 그리고 Eureka의 개념에 대해 간단하게 설명했지만, Eureka의 활용도는 무궁무진하며 Service Discovery & Registry란 개념은 다음 장에서 설명하게 될 Netflix의 다른 component인 Hystrix, Ribbon, Zuul과 결합되어 질 때 활용도가 매우 높아진다.

Eureka - Server
----------------
참고 : https://github.com/phantasmicmeans/Spring-Cloud-Netflix-Eureka-Tutorial/

Reference
----------------
- [Part 1: Using Netflix Eureka, Ribbon and Zuul](https://callistaenterprise.se/blogg/teknik/2015/04/10/building-microservices-with-spring-cloud-and-netflix-oss-part-1/)
- [Part 2: Trying out the circuit breaker, Netflix Hystrix](https://callistaenterprise.se/blogg/teknik/2015/04/15/building-microservices-with-spring-cloud-and-netflix-oss-part-2/)
- [Part 3: Secure API’s with OAuth 2.0](https://callistaenterprise.se/blogg/teknik/2015/04/27/building-microservices-part-3-secure-APIs-with-OAuth/)
- [Part 4: Dockerize your Microservices](https://callistaenterprise.se/blogg/teknik/2015/06/08/building-microservices-part-4-dockerize-your-microservices/)
- [Part 5: Upgrade to Spring Cloud 1.1 & Docker for Mac](https://callistaenterprise.se/blogg/teknik/2016/09/30/building-microservices-part-5-springcloud11-docker4mac/)
- [Part 6: Adding a Configuration Server](https://callistaenterprise.se/blogg/teknik/2017/05/12/building-microservices-part-6-configuration-server/)
- [Part 7: Distributed tracing with Zipkin and Spring Cloud Sleuth](https://callistaenterprise.se/blogg/teknik/2017/07/29/building-microservices-part-7-distributed-tracing/)
- [Part 8: Centralized logging with the ELK stack](https://callistaenterprise.se/blogg/teknik/2017/09/13/building-microservices-part-8-logging-with-ELK/)
