---
date: 2018-09-10
title: Creating and Modeling Validations
categories:
  - Documentation
type: Document
showSidebar: true
published: true
nav_ordering: 4
pageTitle: Creating and Modelling Validations
desc: Details on modelling the data validations for Registry
---

## Overview

OpenSABER validates any record that is inserted or updated in the Registry is validated. Each field in the incoming record is validated using [JSON Schema](https://json-schema.org/) mechanism. The validator we use supports draft 07 of the JSON Schema [specificiation](https://json-schema.org/specification.html).

## Modeling Schema

OpenSABER uses [Everit Schema validator](https://github.com/everit-org/json-schema) for validation. The schema file needs to be created and pre-deployed in the registry under src\main\resources. You can take a look at these examples pre-built into the registry for reference purposes and you may add your own. 

The following reference sample schemas can be found [here](https://github.com/project-sunbird/open-saber/tree/master/java/registry/src/main/resources/public/_schemas) 
* Teacher
* Person
* Vehicle

To quickly understand these schema files in detail, we suggest you take a look at this [README](https://github.com/everit-org/json-schema/blob/master/README.md) of Everit validator.

For more details, look at validation [specification](https://datatracker.ietf.org/doc/draft-handrews-json-schema-validation/)

For a quick and easy schema generation, supply an example payload to this [online schema generator](http://jsonschema.net/) and it will create a rough schema for you.

You can additionally decorate the schema specific to OpenSABER in the following way. This can be found in the reference example - [Teacher schema](https://github.com/project-sunbird/open-saber/tree/master/java/registry/src/main/resources/public/_schemas/Teacher.json)
  
```{
"_osConfig": {
         "osComment": ["This section contains the OpenSABER specific configuration information", 
                      "privateFields: Optional; list of field names to be encrypted and stored in database", 
                      "signedFields: Optional; list of field names that must be pre-signed",
                      "indexFields: Optional; list of field names used for creating index",
                      "uniqueIndexFields: Optional; list of field names used for creating unique index. Field names must be different from index field name"],                     
         "privateFields": ["nationalIdentifier", "teacherCode", "birthDate"],
         "signedFields": ["serialNum"],
         "indexFields": ["nationalIdentifier"],
         "uniqueIndexFields": ["serialNum"]  
}
