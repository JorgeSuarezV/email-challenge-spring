# Email Challenge Spring

In this example you'll find an already setted up empty spring server. Fro this challenge, you'll have to create a service that accepts the necessary information and stores emails.

## Users and Authentication
Users must register first to use the API. User login must be using a username password flow.
Users should be authenticated to make requests to the API. You must implement JWT authentication for this service. JWT token must expire after 1 hour.

## Stats
Only the Admin user for the service can call a /stats endpoint which will retrun a list of all the users and the number of emails they have sent during that day, users who have not used the service should be filtered out.
If a non admin user makes a request for stats they should get a 403 Forbidden error.

## Setup

- Install [Git](https://git-scm.com/), [Docker](https://www.docker.com/), [Java v17](https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html)
- Clone this repository
- Run:
  ```
  ./gradlew build
  ```
- Run:
  ```
  docker compose up
  ```
- You're ready to go!
- To check if your server is running visit http://localhost:8080/api/health in your browser or call that endpoint in Postman

## Useful tools

- An API test tool, you can use the curl command or [Postman](https://www.postman.com/)
- A Database IDE, you can use [PgAdmin](https://www.pgadmin.org/), [Postico](https://eggerapps.at/postico2/), [DataGrip](https://www.jetbrains.com/datagrip/)

## Stack

### Spring Boot

Spring Boot is a powerful framework for building Java-based applications with ease and efficiency. It provides a simplified and opinionated approach to developing production-ready applications by minimizing boilerplate code and simplifying configuration. It aims to simplify the setup and deployment process, allowing developers to focus more on writing business logic and less on infrastructure concerns.

You can have a server running with the Application Class main function.

```
@SpringBootApplication
public class DemoApplication {

	public static void main(String[] args) {
		SpringApplication.run(DemoApplication.class, args);
	}

}
```

[Spring Boot Docs](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#web)

### Hibernate

Hibernate is an object-relational mapping (ORM) framework for Java that provides a way to map Java classes to database tables, allowing you to work with databases using object-oriented programming techniques without writing SQL queries manually.

[Hibernate Docs](https://hibernate.org/orm/documentation/6.2/)

### JPA
JPA (Java Persistence API) is a specification that provides a standard way to map Java objects to relational databases. JPA is not an ORM framework itself, but it defines a set of interfaces and annotations that ORM frameworks like Hibernate can implement.

[JPA Docs](https://jpa-buddy.com/documentation/spring-data/)

## Code Structure

For every class inside the domain (Repository and Services) we create interface, and use dependency injection in the Controller.

We create Data Transfer Objects (DTOs) to abstract from database representation of an entity.

The structure is based on the [Three Layered Architecture](https://dev.to/blindkai/backend-layered-architecture-514h)

```
src
├── main
│   ├── java
│   │   └── com
│   │       └── example
│   │           └── demo
│   │               ├── common
│   │               │   └── (Shared classes or utilities)
│   │               ├── domain1
│   │               │   ├── controller
│   │               │   │   └── (Controller classes for domain1)
│   │               │   ├── model
│   │               │   │   └── (Model classes for domain1)
│   │               │   ├── repository
│   │               │   │   └── (Repository classes for domain1)
│   │               │   ├── service
│   │               │   │   └── (Service classes for domain1)
│   │               │   └── dto
│   │               │       └── (DTO classes for domain1)
│   │               ├── domain2
│   │               │   ├── controller
│   │               │   │   └── (Controller classes for domain2)
│   │               │   ├── model
│   │               │   │   └── (Model classes for domain2)
│   │               │   ├── repository
│   │               │   │   └── (Repository classes for domain2)
│   │               │   ├── service
│   │               │   │   └── (Service classes for domain2)
│   │               │   └── dto
│   │               │       └── (DTO classes for domain2)
│   │               └── DemoApplication.java
│   └── resources
│       ├── application.properties
│       ├── static
│       └── templates
└── test
    └── java
        └── com
            └── example
                └── demo
                    ├── domain1
                    │   └── (Tests for domain1)
                    └── domain2
                        └── (Tests for domain2)

```

## Existing Endpoints

### Health

Endpoints for checking server health

- `GET api/health`

## Endpoints to Implement

### Auth

Endpoints for user authentication

- `POST api/auth/login`
- `POST api/auth/signup`

### User

Endpoints for getting user information

- `GET api/user` returns recomended users paginated
- `GET api/user/me` returns information about the logged user
- `GET api/user/:user_id` returns information about an user by id
- `DELETE api/user` deletes the logged user

### Mail

Endpoints for getting mail information

- `GET api/mail` returns a list of mails by the user who called the endpoint
- `GET api/mail/:mail_id` returns a mail by id
- `GET api/mail/by_user/:user_id` returns all user mails by id
- `POST api/mail` creates a mail
- `DELETE api/mail/:mail_id` deletes a mail by id

### Admin

Endpoints for getting admin information

- `GET api/admin/stats` Only the Admin user for the service can call a /stats endpoint which will retrun a list of all the users and the number of emails they have sent during that day, users who have not used the service should be filtered out. If a non admin user makes a request for stats they should get a 403 Forbidden error.

## Tasks

Fork this repository and complete the tasks. Then create a PR and start with your tasks.

- [ ] Implement all the endpoints given (You can add more endpoints to add more functionality to your app).
- [ ] Create unit tests for your services with JUnit. Make a CI/CD pipeline using github actions to run those tests.
- [ ] Add swagger documentation to some endpoints of your REST API.
