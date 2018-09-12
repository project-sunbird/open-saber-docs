---
date: 2018-09-10
title: Creating and Modelling Validations
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

Data validation is a key part of every application. An application should be capable of verifying the data that is sent to it. After verifying the data, if the data is valid, it should allow the request to be processed and if not, respond with an appropriate message. Currently in Opensaber, any record that is inserted or updated in the Registry is validated. Each field in the incoming record is validated using [Shaclex Validator](http://labra.weso.es/shaclex/){:target="_blank"}. This validator is build using Scala and it is capable of validating [RDF](https://www.w3.org/RDF/){:target="_blank"} data.

## Modelling Validations

[Shaclex Validator](http://labra.weso.es/shaclex/){:target="_blank"} uses a schema for validating a record. The schema file needs to be manually created and configured for the validation to kick-in. In Registry we use 2 schema files for validation, [validations_create.shex](https://github.com/project-sunbird/open-saber/blob/master/java/registry/src/main/resources/validations_create.shex.sample){:target="_blank"} and [validations_update.shex](https://github.com/project-sunbird/open-saber/blob/master/java/registry/src/main/resources/validations_update.shex.sample){:target="_blank"}. [validations_create.shex](https://github.com/project-sunbird/open-saber/blob/master/java/registry/src/main/resources/validations_create.shex.sample){:target="_blank"} is used to validate all records that are inserted into the registry. [validations_update.shex](https://github.com/project-sunbird/open-saber/blob/master/java/registry/src/main/resources/validations_update.shex.sample){:target="_blank"} is used to validate all records that are updated in a registry. To understand these schema files in detail, some of the types of validations which have been modelled in Registry are described with examples below.

### Few Types of Validations Used in Registry

The validations schema is modelled based on the data that needs to be inserted or updated in the Registry. Fields are grouped using Shape expressions. Shape expressions are used to define a bunch of named constraints for each of the fields that need to be validated. Some of the types of constraints used in Registry are mentioned below.

#### CLOSED Shape

This constraint is used to validate the field name as expected by the application. When the Shape is defined as a CLOSED shape in the shape expressions(ShEx) schema file, the validator verifies that the fields in the request, match the fields defined within the Shape. If any field specified in the request is missing from the corresponding shape expression defined in the schema, then data would be termed as invalid because an unidentified field was sent in the request.

##### Example

Consider a relational database with a User table consisting of 5 columns - ```id, givenName, familyName, email, telephone```. In this case, in order to validate the data for insertion into this table, we need to create a Shape Expressions(ShEx) schema file as shown below. The CLOSED constraint is added to Shape definition below.

```
PREFIX sample: <http://example.com/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX schema: <http://schema.org/>

sample:PersonShape CLOSED {
    a [schema:Person] ;
    schema:givenName schema:Text ;
    schema:familyName schema:Text ;
    schema:email schema:Text ;
    schema:telephone schema:Text 
}

```

A request to insert data into this table as shown below would be treated as valid as all the fields in the incoming request match the validation schema above. If in the below request ```telephone``` field name is replace with ```phone``` keyword which is not defined in the validation schema, the request would be termed as invalid due to the CLOSED constraint. When the CLOSED constraint is removed from the shape definition, by default OPEN constraint is applied and any field that is sent in the request would be processed.

```
{
   "@context": {
            "rdf": "http://www.w3.org/1999/02/22-rdf-syntax-ns#",
            "rdfs": "http://www.w3.org/2000/01/rdf-schema#",
            "xsd": "http://www.w3.org/2001/XMLSchema#"
            "schema": "http://schema.org/"
    },
   "schema:givenName":{
	"@type":"schema:Text",
	"@value":""
   }
   "schema:familyName":{
	"@type":"schema:Text",
	"@value":""
   }
   "schema:email":{
	"@type":"schema:Text",
	"@value":""
   }
   "schema:telephone":{
	"@type":"schema:Text",
	"@value":""
   }

}

```

#### Datatype Validation

In order to verify whether the field is of the required datatype as expected by the application, this validation is used. In the above [example](#example), you can see the datatypes - ```schema:Text``` defined for each of the fields. If there is a mismatch between the datatype sent in the request and the datatype specified in the validation schema, the input data would be considered invalid.

#### Cardinality Validation

This validation is used to verify the number of values associated to a field. By default in the above [example](#example), you can see that no cardinality is defined. So when cardinality is not specified, the schema defaults it to 1, which means that each of the 4 fields are mandatory and requires exactly 1 value to be sent for each of the fields.

Below is an example indicating the cardinality.

```
PREFIX sample: <http://example.com/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX schema: <http://schema.org/>

sample:PersonShape CLOSED {
    a [schema:Person] ;
    schema:givenName schema:Text ;
    schema:familyName schema:Text ;
    schema:email schema:Text {1,2};
    schema:telephone schema:Text {2};
    schema:address schema:Text *
}

```

##### Cardinality Description

1. ```{1,2}``` - This indicates the cardinality specified by the pattern {min,max}, where min and max indicates the minimum and the maximum cardinality. Here, the field needs to be sent with exactly 1 value or an array consisting of 2 values.
2. ```{2}``` - Exactly an array of 2 values should be sent for this field.
3. ```*``` - The field can have 0 or any number of values, which means that the field is non-mandatory and it can also be sent with a array consisting of any number of values.

## Summary
 
There are different types of constraints that can be used for validation, such as numeric constraints which allow you to restrict the minimum and maximum value for the field, the number of digits a field can have and so on. More details on these constraints and their usages can be found [here](https://shex.io/shex-primer/){:target="_blank"}.


