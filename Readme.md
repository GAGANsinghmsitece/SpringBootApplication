# Documentation :-

This file will include all the steps required to get started with spring boot 3.

## A simple Spring Boot Application:-

```java
package com.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Main {
    public static void main(String[] args) {
        SpringApplication.run(Main.class, args);
    }
}
```

1. `@SpringBootApplication`:- To declare a class as Spring Boot Application, we need to use `@SpringBootApplication`
   annotation.
2. `SpringApplication`:- It is used to run a server by passing class and argument from command line.

## What is Tomcat server?

Tomcat is a embedded server which comes with the spring boot application. You can also switch to a different server too.

## How to configure a server?

To configure a server, create a file called `application.yml` under `src/main/resources`. Now, you can configure your
server here. For example, if you want to change your port, write following:-

```yml
server:
  port: 8000
```

You can see the full list of options in the official docs.

## Create First Endpoint:-

To Create a endpoint, we first need to specify a class as `RestController` and then we need to map it's method to
corresponding endpoints using `GetMapping` method.
Here's a sample code to do so:-

```java

@SpringBootApplication
@RestController
public class Main {
    public static void main(String[] args) {
        SpringApplication.run(Main.class, args);
    }

    @GetMapping("/")
    public String HomePage() {
        return "Hello World!!!";
    }
}
```

If we go to [localhost:8000](http://localhost:8000), we should see `Hello World!!!`

## How to return complex JSON response?

You can return a JSON expression as follows:-

```java
@GetMapping("/greet")
public Details GreetingPage(){
        Details response=new Details(
        "Hello",
        List.of("Java","C++","Python"),
        new Person("Mike")
        );
        return response;
        }

record Person(String name) {
}

record Details(
        String greet,
        List<String> favProgrammingLanguage,
        Person person
) {
}
```

It will return a response as follows:-

```JSON
{
  "greet": "Hello",
  "favProgrammingLanguage": [
    "Java",
    "C++",
    "Python"
  ],
  "person": {
    "name": "Mike"
  }
}
```

## Useful Commands to manage databases

```shell
docker exec -it postgres bash
psql -U demouser
\l to list databases
CREATE DATABASE customer;
\q
ctrl+D to exit
\c customer // to connect to the database
```