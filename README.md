# Spring Boot 3 - Complete Guide

> **Stack**: Spring Boot **3.4.4** · Java **21** · Spring Framework 6 · Jakarta EE 10

A comprehensive, hands-on reference covering every major Spring Boot concept — from basics to production-grade patterns. Each module is a self-contained, runnable project.

---

## What's Inside

| # | Module | Concept |
|---|--------|---------|
| 1 | `springboot2-annotation-config` | Annotation-based Dependency Injection |
| 2 | `springboot2-xml-config` | XML-based bean configuration |
| 3 | `springboot2-java-config` | Java `@Configuration` classes |
| 4 | `spring-propertysource-example` | `@PropertySource` & `@Value` |
| 5 | `springboot2-externalizing-conf-properties` | Externalised configuration (`application.properties`) |
| 6 | `spring-boot-crud-rest` | CRUD REST API with MySQL & JPA |
| 7 | `springboot-crud-rest-api-validation` | Bean Validation (`@Valid`, JSR-380) |
| 8 | `springboot2-jpa-h2-crud-example` | JPA + H2 in-memory database |
| 9 | `springboot2-jpa-crud-example` | JPA + MySQL CRUD |
| 10 | `springboot2-jpa-auditing` | Spring Data JPA auditing (`@CreatedDate`, `@LastModifiedDate`) |
| 11 | `springboot2-jpa-swagger2` | OpenAPI 3 docs with SpringDoc (`/swagger-ui.html`) |
| 12 | `springboot-mongodb-crud` | Spring Data MongoDB CRUD |
| 13 | `springboot2-mssql-jpa-hibernate-crud-example` | JPA + Microsoft SQL Server |
| 14 | `springboot2-postgresql-jpa-hibernate-crud-example` | JPA + PostgreSQL |
| 15 | `springboot2-jdbc-crud-mysql-example` | Spring JDBC Template |
| 16 | `springboot2-mybatis-mysql-example` | MyBatis ORM |
| 17 | `springboot-multiple-datasources` | Multiple DataSource configuration |
| 18 | `springboot-crud-hibernate-example` | Plain Hibernate (SessionFactory) |
| 19 | `springboot-hibernate-one-one-mapping` | `@OneToOne` JPA mapping |
| 20 | `springboot-hibernate-one-many-mapping` | `@OneToMany` / `@ManyToOne` |
| 21 | `springboot-hibernate-many-to-many-mapping` | `@ManyToMany` + `@JoinTable` |
| 22 | `springboot-hibernate-composite-key-demo` | Composite primary keys (`@EmbeddedId`) |
| 23 | `springboot-jpa-one-to-one-example` | JPA one-to-one (alternative mapping) |
| 24 | `springboot-thymeleaf-hello-world-example` | Thymeleaf template basics |
| 25 | `springboot2-webapp-thymeleaf` | Full MVC web app with Thymeleaf + JPA |
| 26 | `springboot-jsp-hello-world-example` | JSP view basics |
| 27 | `springboot2-webapp-jsp` | Full MVC web app with JSP + JPA |
| 28 | `springboot2-webapp-jsp-WAR` | WAR packaging for external Tomcat |
| 29 | `springboot2-freemarker-example` | FreeMarker template engine |
| 30 | `springboot-thymeleaf-security-demo` | Role-based Spring Security + Thymeleaf |
| 31 | `login-registration-springboot-hibernate-jsp-auth` | User registration & login (JSP) |
| 32 | `spring-aop-advice-examples` | AOP advice types (Before, After, Around) |
| 33 | `springboot2-springaop-example` | Spring AOP with `@Aspect` & Actuator |
| 34 | `springboot-async-example` | Async methods (`@Async`, `CompletableFuture`) |
| 35 | `springboot2-logging` | SLF4J + Logback + Log4j2 |
| 36 | `springboot2-jms-activemq` | JMS messaging with ActiveMQ |
| 37 | `springboot-stomp-websocket` | Real-time WebSocket with STOMP |
| 38 | `springboot-upload-download-file-database` | File upload/download stored in DB |
| 39 | `springboot-upload-download-file-rest-api-example` | File upload/download REST API |
| 40 | `springboot2-junit5-example` | Unit & integration testing with JUnit 5 |
| 41 | `springboot-testing-examples` | `@DataJpaTest`, `@WebMvcTest`, `TestRestTemplate` |
| 42 | `springboot-angular8-helloworld-example` | Spring Boot REST backend + Angular frontend |

---

## Spring Boot 3 Migration Notes

This project has been upgraded from Spring Boot 2.x to **Spring Boot 3.4.4** running on **Java 21**. Key changes:

| Old | New |
|-----|-----|
| `spring-boot-starter-parent 2.x` | `spring-boot-starter-parent 3.4.4` |
| Java 8 | Java 21 (LTS) |
| `javax.persistence.*` | `jakarta.persistence.*` |
| `javax.validation.*` | `jakarta.validation.*` |
| `javax.servlet.*` | `jakarta.servlet.*` |
| `mysql:mysql-connector-java` | `com.mysql:mysql-connector-j` |
| Springfox Swagger 2 | SpringDoc OpenAPI 3 (`springdoc-openapi-starter-webmvc-ui`) |
| `thymeleaf-extras-springsecurity4` | `thymeleaf-extras-springsecurity6` |
| `javax.servlet:jstl` | `org.glassfish.web:jakarta.servlet.jsp.jstl` |
| `com.microsoft.sqlserver:sqljdbc4:4.0` | `com.microsoft.sqlserver:mssql-jdbc` (managed by Boot BOM) |
| MyBatis starter `1.2.1` | MyBatis starter `3.0.3` |
| Gradle `compile` / `testCompile` | `implementation` / `testImplementation` |

---

## Prerequisites

| Tool | Minimum Version |
|------|----------------|
| JDK | 21 |
| Maven | 3.9+ |
| Gradle | 8.x (stomp-websocket module) |
| Docker (optional) | any recent version |

---

## Quick Start

```bash
# Clone
git clone https://github.com/sandipsmenon/spring-boot-tutorial.git
cd spring-boot-tutorial

# Run any module (example: H2 in-memory CRUD — no DB setup needed)
cd springboot2-jpa-h2-crud-example
mvn spring-boot:run
```

Modules that need MySQL/PostgreSQL/MSSQL require a running database. Update `src/main/resources/application.properties` with your credentials before running.

---

## Concepts Reference

### 1. Spring Boot Fundamentals
- Auto-configuration (`@SpringBootApplication`, `@EnableAutoConfiguration`)
- Dependency Injection: annotation config, Java `@Configuration`, XML config
- Bean lifecycle & scopes
- `application.properties` / `application.yml`, profiles (`@Profile`)
- `@PropertySource`, `@ConfigurationProperties`, `@Value`

### 2. REST API Development
- `@RestController`, `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`
- `ResponseEntity`, `@RequestBody`, `@PathVariable`, `@RequestParam`
- Global exception handling (`@ControllerAdvice`, `@ExceptionHandler`)
- Bean Validation (`@Valid`, `@NotNull`, `@Size`, `@Email`)
- OpenAPI 3 documentation with SpringDoc

### 3. Data Access
- Spring Data JPA (`JpaRepository`, `CrudRepository`, `PagingAndSortingRepository`)
- Hibernate ORM (entity mappings, relationships, composite keys)
- JPA Auditing (`@EnableJpaAuditing`, `@CreatedDate`, `@LastModifiedDate`)
- Spring JDBC Template
- MyBatis
- Spring Data MongoDB
- Multiple DataSources

### 4. JPA Entity Relationships
- `@OneToOne`, `@OneToMany`, `@ManyToOne`, `@ManyToMany`
- Cascade types, fetch strategies (EAGER/LAZY)
- `@JoinColumn`, `@JoinTable`
- `@EmbeddedId` composite keys

### 5. Web Application (MVC)
- Spring MVC (`@Controller`, `@RequestMapping`, `Model`, `ModelAndView`)
- Thymeleaf (templates, fragments, layouts, form binding)
- JSP + JSTL
- FreeMarker
- Form validation in MVC (`@Valid`, `BindingResult`)
- WAR deployment to external Tomcat

### 6. Spring Security
- HTTP Basic & form-based authentication
- Role-based access control (`@PreAuthorize`, `hasRole()`)
- `UserDetailsService`, `PasswordEncoder` (BCrypt)
- CSRF protection
- Security with Thymeleaf (`thymeleaf-extras-springsecurity6`)
- User registration & login flows

### 7. Aspect-Oriented Programming (AOP)
- `@Aspect`, `@Pointcut`
- Advice types: `@Before`, `@After`, `@AfterReturning`, `@AfterThrowing`, `@Around`
- Use cases: logging, performance monitoring, transactions

### 8. Asynchronous Processing
- `@EnableAsync`, `@Async`
- `CompletableFuture` return types
- Custom thread pool (`ThreadPoolTaskExecutor`)

### 9. Messaging
- JMS with ActiveMQ (`@JmsListener`, `JmsTemplate`)
- WebSocket with STOMP (`@MessageMapping`, `SimpMessagingTemplate`)
- Real-time messaging to browser clients

### 10. File Handling
- Multipart file upload (`@RequestParam MultipartFile`)
- File download (`InputStreamResource`, `ByteArrayResource`)
- Storing files in database (as BLOB)
- Storing files in filesystem

### 11. Testing
- `@SpringBootTest` (full integration tests)
- `@WebMvcTest` (controller slice tests)
- `@DataJpaTest` (repository slice tests)
- `MockMvc`, `TestRestTemplate`, `WebTestClient`
- JUnit 5 (`@Test`, `@BeforeEach`, `@ExtendWith`, `@ParameterizedTest`)
- Mockito (`@Mock`, `@MockBean`, `@InjectMocks`)

### 12. Logging & Monitoring
- SLF4J + Logback (default in Spring Boot)
- Log4j2 configuration
- Log levels, rolling file appenders
- Spring Boot Actuator endpoints (`/actuator/health`, `/actuator/info`, `/actuator/metrics`)

### 13. API Documentation
- SpringDoc OpenAPI 3 (`@Operation`, `@ApiResponse`, `@Schema`)
- Swagger UI at `/swagger-ui/index.html`
- OpenAPI JSON spec at `/v3/api-docs`

### 14. Frontend Integration
- CORS configuration (`@CrossOrigin`, `CorsConfigurationSource`)
- Spring Boot as REST backend for Angular / React / Vue
- WebJars for serving frontend libraries (Bootstrap, jQuery)

---

## Database Quick Reference

| Module | Database |
|--------|----------|
| `*-h2-*` | H2 (embedded, no setup needed) |
| `*-mysql-*`, `spring-boot-crud-rest` | MySQL 8+ |
| `*-postgresql-*` | PostgreSQL 15+ |
| `*-mssql-*` | SQL Server 2019+ |
| `springboot-mongodb-crud` | MongoDB 6+ |

---

## Project Structure

Each module follows standard Maven layout:

```
module-name/
├── src/
│   ├── main/
│   │   ├── java/         # Application code
│   │   └── resources/
│   │       └── application.properties
│   └── test/
│       └── java/         # Test code
└── pom.xml
```

---

## Contributing

Pull requests welcome. Please keep each module focused on demonstrating a single Spring Boot concept.

---

## License

This project is open-source and available for educational use.
