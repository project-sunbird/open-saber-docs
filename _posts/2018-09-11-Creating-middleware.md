---
date: 2018-09-10
title: Creating Middleware
categories:
  - Documentation
type: Document
showSidebar: true
published: true
nav_ordering: 13
pageTitle: "Creating Middleware"
---
## STEPS TO CREATE MIDDLEWARE

1. Clone the git repository for [open-saber](https://github.com/project-sunbird/open-saber){:target="_blank"}

2. Create a new maven project inside java/middleware/registry-middleware folder, with registry-middleware artifact as the parent for this project

```
<parent>
    <groupId>io.opensaber</groupId>
    <artifactId>registry-middleware</artifactId>
    <version>0.0.1-SNAPSHOT</version>
</parent>
```

3. Include middleware-commons as a dependency in the pom.xml file of this project

```
<dependency>
    <groupId>io.opensaber</groupId>
    <artifactId>middleware-commons</artifactId>
    <version>0.0.1-SNAPSHOT</version>
</dependency>

```
4. Create a java class implementing the [Middleware](https://github.com/project-sunbird/open-saber/blob/master/java/middleware-commons/src/main/java/io/opensaber/registry/middleware/Middleware.java){:target="_blank"} interface.

5. Implement the **execute()** method to include the logic/functionality for the middleware.
6. Currently the **next()** method is not being used in the middleware, so an empty implementation can be added for now.

7. Modify the [pom.xml](https://github.com/project-sunbird/open-saber/blob/master/java/middleware/registry-middleware/pom.xml){:target="_blank"} file in [registry-middleware](https://github.com/project-sunbird/open-saber/tree/master/java/middleware/registry-middleware){:target="_blank"} to include this newly created middleware artifact as a module

8. Modify the [pom.xml](https://github.com/project-sunbird/open-saber/blob/master/java/middleware/pom.xml){:target="_blank"} in [middleware](https://github.com/project-sunbird/open-saber/blob/master/java/middleware){:target="_blank"} to specify the version and the dependency for this newly created artifact



