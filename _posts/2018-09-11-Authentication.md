---
date: 2018-09-10
title: Authentication
categories:
  - Documentation
type: Document
showSidebar: false
published: false
nav_ordering: 9
pageTitle: "Authentication"
---
## Overview

We can look at application authentication to be largely falling into the following buckets:
1. Local Authentication, where the user and credentials are managed local to the application.
2. Identity Provider (IdP) based Authentication, where the authentication is done by a separate Provider and user credentials are not stored in the Application.

OpenSABER APIs would need a client to make calls on behalf of the user. The client could be a server, a mobile app, javascript on a single page app, a command line utility, etc.

Let's talk about the IdP case first, where we will talk about how to integrate OpenSABER in an existing system which has an IdP.

### via App in the same domain

Following is a case where Registry is being accessed via an OAuth / OpenID Connect flow, where the IdP and App both belong to the same domain. 

[![Single Domain Auth](/images/AuthorizationFlowSingleDomain.png)](/images/AuthorizationFlowSingleDomain.png){:target="_blank"}

Note that the IdP performs an OAuth Delegation and uses OpenID Connect flow to issue an ID Token and Auth token (with claims) to the App which is used by the App to (1) create a Session and (2) transfer the ID and the claim respectively to the Registry whenever an access to the Registry is required in that Session. The App needs to handle cases where the Access Token is denied by the Registry.


