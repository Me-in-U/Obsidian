# 3일차

## Spring Legacy vs Spring Boot 차이

| 구분       | Spring Legacy                       | Spring Boot                                                             |
| -------- | ----------------------------------- | ----------------------------------------------------------------------- |
| 설정 방식    | XML·JavaConfig 수동 등록 (100줄↑ XML 흔함) | `application.properties`/`yml`, Auto‑Configuration 기반 (설정 파일 수십 줄로 최소화) |
| 서버 실행 방식 | 외부 톰캣 설치·WAR 배포 -> 재기동              | 내장 톰캣/Jetty(독립 실행 가능) → `java -jar` 또는 IDE 실행 (배포 패키지 단일 JAR)           |
| 의존성 관리   | 개별 라이브러리 버전 충돌 해결 직접 수행             | `spring-boot-starter-*` 사용, BOM(Bill of Materials)이 라이브러리 버전을 검증·고정     |
| 개발 생산성   | 초기 설정·XML 작성에 평균 2~3일 소요 (추측)       | 프로젝트 생성부터 기동까지 5분 이내 가능, 스타터 제공으로 코드량↓·실험 빠름                            |
**장점·단점**  
- **Spring Legacy 장점**: 세밀한 설정 제어 가능, 레거시 환경 호환성(자바 EE 서버 등)  
- **Spring Legacy 단점**: 초기 설정 장벽 높음(XML 장황, 버전 충돌)  
- **Spring Boot 장점**: 빠른 개발·배포, 일관된 의존성 관리, 풍부한 스타터·Actuator  
- **Spring Boot 단점**: Auto‑Configuration 과다 시 디버깅 난이도 증가, 내부 동작 추적 필요  


## `application.properties` 역할

> Spring Boot 애플리케이션의 서버 포트·데이터소스·로깅 레벨·프로파일 등 핵심 환경 설정과 Auto‑Configuration 조정을 중앙에서 관리하는 구성 파일

1. 애플리케이션 기본 정보: `spring.application.name`, `spring.profiles.active`
2. 서버 설정: `server.port`, `server.servlet.context-path`
3. 데이터소스 & JPA: `spring.datasource.url`, `spring.jpa.hibernate.ddl-auto`
4. 로깅: `logging.level.com.ssafy`, `logging.pattern.console`
5. 웹(MVC/HTTP): `spring.mvc.view.prefix`, `spring.http.encoding.charset`
6. 보안(Security): `spring.security.user.name`, `spring.security.oauth2.client.client-id`
7. 운영·모니터링(Actuator): `management.endpoints.web.exposure.include`, `management.endpoint.health.show-details`
8. 스타터별 기능: `spring.mail.host`, `spring.cache.type`
9. 커스텀 프로퍼티: `app.upload.dir`, `my.company.feature.enabled`

## `@SpringBootApplication` 내부 어노테이션

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@SpringBootConfiguration    // 1
@EnableAutoConfiguration    // 2
@ComponentScan              // 3
public @interface SpringBootApplication { … }
```

1. `@SpringBootConfiguration` - `@Configuration` 상속, 스프링 빈 정의(Bean Definition) 클래스 역할
2. `@EnableAutoConfiguration` - 클래스패스(Classpath)·설정(Property) 기반 자동 설정(자동 빈 등록)
3. `@ComponentScan` - 현재 패키지 및 하위 패키지의 `@Component`, `@Service`, `@Repository` 등을 스캔

나머지는 JVM 메타데이터 용도
