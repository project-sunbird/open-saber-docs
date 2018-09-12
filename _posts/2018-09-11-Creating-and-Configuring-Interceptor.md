---
date: 2018-09-10
title: Creating and Configuring Interceptor
categories:
  - Documentation
type: Document
showSidebar: true
published: true
nav_ordering: 11
pageTitle: "Creating and Configuring Interceptor"
---
## STEPS TO CREATE INTERCEPTOR

1. Clone the git repository for open-saber

2. Create a new interceptor class in [registry-interceptor](https://github.com/project-sunbird/open-saber/blob/master/java/registry-interceptor){:target="_blank"} package

3. This class should implement Spring framework's [HandlerInterceptor](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/web/servlet/HandlerInterceptor.html){:target="_blank"} interface and override the preHandle, postHandle and afterCompletion on need basis

4. This class can also extend the [BaseRequestHandler](https://github.com/project-sunbird/open-saber/blob/master/java/registry-interceptor/src/main/java/io/opensaber/registry/interceptor/handler/BaseRequestHandler.java){:target="_blank"} or [BaseResponseHandler](https://github.com/project-sunbird/open-saber/blob/master/java/registry-interceptor/src/main/java/io/opensaber/registry/interceptor/handler/BaseResponseHandler.java){:target="_blank"} to manage requests and response

5. In order to use the middleware within this interceptor, we can modify the [pom.xml](https://github.com/project-sunbird/open-saber/blob/master/java/registry-interceptor/pom.xml){:target="_blank"} in this package to include the dependency

## STEPS TO CONFIGURE INTERCEPTOR

1. Configuration for the interceptor can be added in [GenericConfiguration](https://github.com/project-sunbird/open-saber/blob/b09b444f08ce56f19049e7ae672f9290fd688217/java/registry/src/main/java/io/opensaber/registry/config/GenericConfiguration.java#L208){:target="_blank"} class
 
2. While adding this configuration, the route needs to be specified, if not, it would apply to all routes
