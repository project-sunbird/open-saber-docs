---
date: 2018-09-10
title: Generate authentication token for accessing APIs
categories:
  - Documentation
type: Document
showSidebar: false
published: false
nav_ordering: 14
pageTitle: "Generate authentication token for accessing APIs"
---

## Steps to generate auth-token
 Following are the steps to authenticate a user when the user is supposed to access any OpenSABER APIs.

`Step 1 `:  Set environment variables
 ```bash
Linux/Mac OS - set following key-value pairs in your bash profile or /etc/environment
 Windows(version 7 and above) OS- Control Panel->System and Security ->Advance system settings -> Environment Variables-> New (under System Variable section) 
```
 Set these key-value pairs as environment variables
```bash
sunbird_sso_publickey = ******
sunbird_sso_realm=sunbird
sunbird_sso_url=https://dev.open-sunbird.org/auth/
sunbird_sso_username=******
sunbird_sso_password=******
sunbird_sso_client_id=admin-cli 
```

`Step 2`: Generate access token using the following command    
```bash
curl -X POST https://dev.open-sunbird.org/auth/realms/sunbird/protocol/openid-connect/token -H 'cache-control: no-cache' -H 'content-type: application/x-www-form-urlencoded' -d 'client_id=admin-cli&username=******&password=******&grant_type=password'
```

`Step 3`: While invoking any API of OpenSABER, use the value of "**access-token**" from step 2 along with key as "**x-authenticated-user-token**"  in HTTP header.
