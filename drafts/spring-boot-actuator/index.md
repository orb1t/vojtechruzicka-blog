---
title: 'Actuator: Spring Boot Production Monitoring and Management'
date: "2018-08-24T22:12:03.284Z"
tags: ['Spring', 'Java']
path: '/spring-boot-actuator'
featuredImage: './spring-boot-actuator.jpg'
disqusArticleIdentifier: '99008 http://vojtechruzicka.com/?p=99008'
excerpt: 'Monitor and manage your application in production with Spring Boot Actuator. Gather metrics or check health easily.'
---

![Spring Boot Actuator](spring-boot-actuator.jpg)

# Basic build information
In one of my previous articles, I described ho to obtain some basic information about the current build of the application at runtime in spring boot.

<div class="linked-post"><h4 class="front-post-title" style="margin-bottom:0.375rem;" data-reactid="21"><a style="box-shadow:none;" href="/spring-boot-version/" data-reactid="22">Detecting build version and time at runtime in Spring Boot</a></h4><small class="front-post-info" data-reactid="23"><span class="front-post-info-date" data-reactid="24">25 June, 2018</span><div class="post-tags" data-reactid="25"><ul data-reactid="26"><li data-reactid="27"><a href="/tags/spring" data-reactid="28"><!-- react-text: 29 -->#<!-- /react-text --><!-- react-text: 30 -->Spring<!-- /react-text --></a></li></ul></div></small><div data-reactid="31"><a class="front-post-image" href="/spring-boot-version/" data-reactid="32"><div class=" gatsby-image-outer-wrapper" style="position:relative;" data-reactid="33"><div class=" gatsby-image-wrapper" style="position:relative;overflow:hidden;" data-reactid="34"><div style="width:100%;padding-bottom:66.5%;" data-reactid="35"></div><img alt="" src="data:image/jpeg;base64,/9j/2wBDABALDA4MChAODQ4SERATGCgaGBYWGDEjJR0oOjM9PDkzODdASFxOQERXRTc4UG1RV19iZ2hnPk1xeXBkeFxlZ2P/2wBDARESEhgVGC8aGi9jQjhCY2NjY2NjY2NjY2NjY2NjY2NjY2NjY2NjY2NjY2NjY2NjY2NjY2NjY2NjY2NjY2NjY2P/wgARCAANABQDASIAAhEBAxEB/8QAGQAAAgMBAAAAAAAAAAAAAAAAAAMBAgQF/8QAFQEBAQAAAAAAAAAAAAAAAAAAAgP/2gAMAwEAAhADEAAAAauyMjSDrCP/xAAaEAADAQADAAAAAAAAAAAAAAAAAQIRAxIT/9oACAEBAAEFAuIqOxjQqcnpRur/xAAWEQEBAQAAAAAAAAAAAAAAAAAAARH/2gAIAQMBAT8Bsa//xAAWEQEBAQAAAAAAAAAAAAAAAAAAARH/2gAIAQIBAT8BlY//xAAbEAACAgMBAAAAAAAAAAAAAAAAIQERAhBBUf/aAAgBAQAGPwKULGV4OKEX3X//xAAbEAEAAgIDAAAAAAAAAAAAAAABABExQRAhUf/aAAgBAQABPyEDslS7GgmIi8eIUZ9IUFDE/9oADAMBAAIAAwAAABDP3//EABYRAQEBAAAAAAAAAAAAAAAAABEBEP/aAAgBAwEBPxCi4//EABYRAQEBAAAAAAAAAAAAAAAAAAEQEf/aAAgBAgEBPxAMCP/EABwQAQACAwADAAAAAAAAAAAAAAEAESExQVFhgf/aAAgBAQABPxAzA7Iioho0/YA8o7CZJhb0uJa101gp2J2ZgCHXqf/Z" style="position: absolute; top: 0px; left: 0px; transition: opacity 0.5s ease 0.25s; width: 100%; height: 100%; object-fit: cover; object-position: center center; opacity: 0;" data-reactid="36"><img alt="" srcset="/static/spring-boot-version-addd7022e57908233618e4c15582fa6e-3c244.jpg 45w,
/static/spring-boot-version-addd7022e57908233618e4c15582fa6e-f58d6.jpg 90w,
/static/spring-boot-version-addd7022e57908233618e4c15582fa6e-f7f9a.jpg 180w,
/static/spring-boot-version-addd7022e57908233618e4c15582fa6e-870e7.jpg 270w,
/static/spring-boot-version-addd7022e57908233618e4c15582fa6e-dbc85.jpg 360w,
/static/spring-boot-version-addd7022e57908233618e4c15582fa6e-ac624.jpg 540w,
/static/spring-boot-version-addd7022e57908233618e4c15582fa6e-7d936.jpg 1600w" src="/static/spring-boot-version-addd7022e57908233618e4c15582fa6e-f7f9a.jpg" sizes="(max-width: 180px) 100vw, 180px" style="position: absolute; top: 0px; left: 0px; transition: opacity 0.5s ease 0s; width: 100%; height: 100%; object-fit: cover; object-position: center center; opacity: 1;"><noscript data-reactid="37"><img src="/static/spring-boot-version-addd7022e57908233618e4c15582fa6e-f7f9a.jpg" srcset="/static/spring-boot-version-addd7022e57908233618e4c15582fa6e-3c244.jpg 45w,
/static/spring-boot-version-addd7022e57908233618e4c15582fa6e-f58d6.jpg 90w,
/static/spring-boot-version-addd7022e57908233618e4c15582fa6e-f7f9a.jpg 180w,
/static/spring-boot-version-addd7022e57908233618e4c15582fa6e-870e7.jpg 270w,
/static/spring-boot-version-addd7022e57908233618e4c15582fa6e-dbc85.jpg 360w,
/static/spring-boot-version-addd7022e57908233618e4c15582fa6e-ac624.jpg 540w,
/static/spring-boot-version-addd7022e57908233618e4c15582fa6e-7d936.jpg 1600w" alt="" sizes="(max-width: 180px) 100vw, 180px" style="position:absolute;top:0;left:0;transition:opacity 0.5s;transition-delay:0.5s;opacity:1;width:100%;height:100%;object-fit:cover;object-position:center"/></noscript></div></div></a><span class="front-post-excerpt" data-reactid="38">How to obtain artifact version, build time and other build information in a Spring Boot app at runtime?</span></div></div>

While this can be handy, it is usually not sufficient. There is a lot more you are usually interested in. And most importantly, it does not involve just the information known at build time, but rather what is the application's current status at runtime. In these situations, you should use Spring Boot Actuator.

# Spring Boot Actuator
In short, Spring Boot Actuator is one of the sub-projects od Spring Boot, which adds Monitoring and Management support for your applications running in production. It exposes various HTTP or JMX endpoints you can interact with.

# Adding Dependencies
Basic setup is really simple, you just need to add one dependency to your project - `spring-boot-starter-actuator`. 

Maven:
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

Gradle:
```
compile("org.springframework.boot:spring-boot-starter-actuator")
```

As usual, once this dependency is on the classpath, Spring Boot is able to detect this and auto-configures Actuator for you. Just rebuild and start your application.

# Up and Running
Now if you run your application, you can check all the available endpoints by accessing `/actuator`. That means, if you are running locally on port 8080, you'll need to open `http://localhost:8080/actuator`. You should see something similar to this:

```json
{
  "_links": {
    "self": {
      "href": "http://localhost:8080/actuator",
      "templated": false
    },
    "health": {
      "href": "http://localhost:8080/actuator/health",
      "templated": false
    },
    "info": {
      "href": "http://localhost:8080/actuator/info",
      "templated": false
    }
  }
}
```

This is the list of all the available Actuator endpoints. As you can see, there is just two of them: health and info. Let's try `/health` first.

```json
{"status":"UP"}
```

And now `/info`. It looks like it is returning just an empty json: `{}`. 

# More endpoints
Not very impressive so far. Of course, Actuator offers much more than this, otherwise it wouldn't be very useful. There are some examples of available endpoints, with the full list available in the [official docs](https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-endpoints.html#production-ready-endpoints).

| Endpoint   | Description   |
|------------|---------------|
| health  | Application health info  |
| info  | Info about the application  |
| env  | Properties from environment  |
| metrics  | Various metrics about the app  |
| mappings  | `@REquestMapping` Controller mappings  |
| shutdown  | Triggers application shutdown  |
| httptrace  | HTTP request/response log  |
| loggers  | Display and configure logger info  |
| logfile  | Contents of the log file  |
| threaddump  | Perform thread dump  |
| heapdump  | Obtain JVM heap dump  |

## Exposing endpoints
For most of the endpoints, Actuator offers two ways of connecting to them:
- HTTP REST endpoint
- JMX endpoint

By default, as we already saw, only *health* and *info* endpoints are exposed over HTTP. However, all of them are exposed over JXM (where applicable) by default.

You can configure in your `application.properties` which endpoints should be exposed:

```properties
# Expose over JMX
management.endpoints.jmx.exposure.exclude=shutdown
management.endpoints.jmx.exposure.include=*
# Expose HTTP REST Endpoint
management.endpoints.web.exposure.exclude=
management.endpoints.web.exposure.include=health,info,metrics
```

As you can see you can define endpoints by name or use `*` to represent all endpoints. You can combine include and exclude filters.

If you change your configuration to expose all the endpoints over HTTP and restart your app, your `/actuator` endpoint will now show many more URLs.

```properties
management.endpoints.web.exposure.include=*
```

## Enabling / Disabling endpoints
You can configure not only whether an endpoint is exposed over HTTP or JMX, you can also turn specific endpoints on/off. All the endpoints except `shutdown` are enabled by default (although not exposed over HTTP).

```properties
# Disable an endpoint
management.endpoint.[endpoint-name].enabled=false

# Specific example for 'health' endpoint
management.endpoint.health.enabled=false

# Instead of enabled by default, you can change to mode
# Where endpoints need to be explicitly enabled
management.endpoints.enabled-by-default=false

```

# Source code
Source code of example application using Spring Boot Actuator can be found [here](https://github.com/vojtechruz/spring-boot-actuator-example).

# Conclusion