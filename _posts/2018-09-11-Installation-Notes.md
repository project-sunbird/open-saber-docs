---
date: 2018-09-10
title: Installation Notes
categories:
  - Documentation
type: Document
showSidebar: false
published: false
nav_ordering: 18
pageTitle: "Installation Notes"
---

## Attempt 1 - July 13th

### Dependencies

 - Had git and java installed, did not verify.
 - Update instructions to indicate that installing dependencies is left to the reader
 - docker compose seems to be required, missing from dependencies
 
## Configuration

 1. Dependency on Keycloak for authentication is missing -- should provide links to Keycloak setup 
 2. Missing instruction on ow to retrieve the Keycloak sso key -- should provide links to retrieving SSO key

## Understanding configuration files
1. Error in the location of the config files

## Running OpenSaber

1. cd path incorrect (already in directory `open-saber/java`)
2. Running via docker

When running `docker-compose up`:

    Traceback (most recent call last):
      File "/usr/local/bin/docker-compose", line 7, in <module>
        from compose.cli.main import main
    ModuleNotFoundError: No module named 'compose'

Investigating docker version

    docker --version
    Docker version 17.12.0-ce, build c97c6d6

3. Running via java target

When executing `cd target` from `open-saber/java/registry`

    -bash: cd: target: No such file or directory

The following target directories are found but unclear which is the intended target

    ./middleware/registry-middleware/rdf-validation-mapping/target
    ./middleware/registry-middleware/rdf-validation/target
    ./middleware/registry-middleware/rdf-conversion/target
    ./middleware/registry-middleware/jsonld-conversion/target
    ./middleware/registry-middleware/authorization/target
    ./middleware-commons/target
    ./schema-configuration/target
    ./converters/jenardf4j/target
    ./converters/rdf2Graph/target
    ./transaction-event-handler/target
    ./opensaber-client/target
    ./validators/shex/shaclex/target
    ./registry-interceptor/target
    ./pojos/target

Attempting to find the jar file:

    find . -iname registry.jar
    No result found


### Result

Blocked, could not start the binary
