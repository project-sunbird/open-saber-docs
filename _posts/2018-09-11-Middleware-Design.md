---
date: 2018-09-10
title: Middleware Design
categories:
  - Documentation
type: Document
showSidebar: false
published: false
nav_ordering: 2
pageTitle: "Middleware Design"
---

## OPENSABER MIDDLEWARE

Opensaber middleware is an independent set of plug-able software components which handles the data that goes into the registry. The middleware will be designed to perform a number of operations such as data manipulation, validation and application of rules specific to each registry. Each functionality will be an independent component and the middleware can be customised in such a way that it could be a mix and match of any number of these components which combine to form the middleware for any registry.


## Features

* Perform token based authentication and authorisation for each request
* Serialize the data
* Perform format changes such as conversions between JSON-LD and RDF formats 
* Validate the incoming request data based on registry specific rules


## Design

Middleware is being currently designed using Interceptors in spring framework. As the name suggests, it intercepts incoming requests and outgoing responses of an application. Thus giving us a control on the data flow within the application. It provides handlers which are capable of manipulating the data within the request and response and also control the data that is sent to the view. Base interface for the middleware is given below.
```
public interface Middleware {
  
	Map<String,Object> execute(Map<String,Object> mapData) throws IOException, MiddlewareHaltException;
	Map<String,Object> next(Map<String,Object> mapData) throws IOException;

}
```
Each middleware we create needs to implement the execute method in the above interface which should include the functionality for the middleware .Currently since we are using interceptors in spring framework to invoke the middleware, the ordering and the chaining is handled through configuration within the framework. Is it also possible to replace this chaining mechanism with a custom chaining approach instead of the interceptor mechanism.

Base classes, [BaseRequestHandler](https://github.com/project-sunbird/open-saber/tree/master/java/registry-interceptor/src/main/java/io/opensaber/registry/interceptor/handler/BaseRequestHandler.java){:target="_blank"} and [BaseResponseHandler](https://github.com/project-sunbird/open-saber/tree/master/java/registry-interceptor/src/main/java/io/opensaber/registry/interceptor/handler/BaseResponseHandler.java){:target="_blank"} have been created for handling request and response data. The middlewares created will make use of these handlers to access the request and response object, manipulate the data within them and create custom requests or responses in order to pass it to the next handler/middleware in the sequence configured. 

Similarly requests and response wrappers, [RequestWrapper](https://github.com/project-sunbird/open-saber/tree/master/java/registry-interceptor/src/main/java/io/opensaber/registry/interceptor/handler/RequestWrapper.java){:target="_blank"} and [ResponseWrapper](https://github.com/project-sunbird/open-saber/tree/master/java/registry-interceptor/src/main/java/io/opensaber/registry/interceptor/handler/ResponseWrapper.java){:target="_blank"} have been created in order to enable reading of the request and response content multiple times, since there could be no middleware or even a sequence of middlewares which will require access to read the request or the response content repeatedly.

Spring interceptor is created by implementing the HandlerInterceptor interface in spring framework. This interface involves three methods - preHandle, postHandle and afterCompletion. 

* preHandle - This method is executed before the handler of the request is invoked, for e.g. the controller in our application.
* postHandle - This method gets invoked after the handler invocation is complete, but before the response is rendered
* afterCompletion - This method gets invoked after the request is completed, mostly used for cleanups

Sample interceptor structure can be found below.
```
public class JsonldToRdfInterceptor implements HandlerInterceptor{

	@Override
	public boolean preHandle(HttpServletRequest request,
	  HttpServletResponse response, Object object) throws Exception {
	}
	@Override
	public void postHandle(HttpServletRequest request,HttpServletResponse response,
	  Object handler, ModelAndView modelAndView) throws Exception {	
	}
	@Override
	public void afterCompletion(HttpServletRequest request, HttpServletResponse response,
	  Object handler, Exception ex) {
	}	`
}
```
## Benefits of using Interceptors

* Interceptors are plug-able and configurable, hence they can be added or removed from the application anytime. 
* They can be customised to run in any order
* They can be customised for each specific route, each route pattern within the application, or the entire application
* Custom ones can be created and configured as required
* They provide access to response before the view is rendered
* They also provide option to do cleanup after the view is rendered


## Examples

### JSON-LD to RDF Converter

This feature accepts data in JSON-LD format and converts to RDF format. Suppose an entity needs to be added to a registry. The data in the request is in JSON-LD format. The data needs to be converted to RDF format before it is saved into the database. This can be handled by an interceptor, which handles every incoming request to save data, validates the JSON-LD format and converts it into RDF before it reaches the handler i.e. the controller of the request.


### RDF to JSON-LD Converter

This feature accepts data in RDF format and converts to JSON-LD format. When an entity is read from the database, it needs to be converted to JSON-LD before the response reaches the view. This can be handled by an interceptor, which handles every outgoing response and converts it into JSON-LD.


### Token Based Authentication and Authorization

A token based authentication is a mechanism by which a unique token is generated for each user and this token is included in every request to authenticate or authorize the user. When a interceptor handles this scenario, it will accept the incoming request, read the token and validate it to authenticate/authorize the user. If the token is invalid, it will not proceed with the request and instead pre-handle it by sending an appropriate response to the user. It will prevent the request from reaching the handler of the request. Since interceptors are configurable, a custom authentication/authorization mechanism could also be used instead of this token based system.
