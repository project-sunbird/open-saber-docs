---
date: 2018-09-10
title: Performance benchmarking and Profiling
categories:
  - Documentation
type: Document
showSidebar: false
published: false
nav_ordering: 16
pageTitle: "Performance benchmarking and Profiling"
---
## STEPS

1. Install [API Bench](https://github.com/apigee/apib){:target="_blank"}. 
2. Set the property [perf.monitoring.enabled](https://github.com/project-sunbird/open-saber/blob/b09b444f08ce56f19049e7ae672f9290fd688217/java/registry/src/main/resources/application.yml.sample#L15){:target="_blank"} to true. This is to enable profiling. 
2. Build and start the registry application.
3. Run the below commands in the base directory of this installation.

## Commands

**1. Add API**

./apib -f **input-file** -c 5 -d 40 -H 'x-authenticated-user-token: **authentication-token**' **URL**

**2. Read API**

./apib -c 30 -d 40 -H 'x-authenticated-user-token: **authentication-token**' **URL**

**Parameters Used**
1. -f - argument to pass the file name which contains the request body.
2. -c - argument to indicate number of concurrent requests.
3. -d - argument to indicate total duration of the test.
4. -H - argument to provide headers in key:value format.
5. input-file - This is the name of the file which contains the request body for this API call.
6. authentication-token - This is the token used for authorising the request. 
7. URL - The URL of the API.


