---
date: 2018-09-10
title: Installation
categories:
  - Documentation
type: Document
showSidebar: true
published: true
nav_ordering: 3
pageTitle: "OpenSaber Installation"
---

## Prerequisites

* Java - 8+
* Git

### Building the library

```sh
git clone https://github.com/project-sunbird/open-saber.git
cd open-saber
sh configure-dependencies.sh
```
This should install default configuration, which will configure resource files required for a default Teacher Registry on your machine.

#### Installing the dependencies

```sh
cd java
mvn clean install
```

### Build registry

```sh
cd registry
mvn clean install
```

## Configurations

#### 1 - Configure environment variables for authentication (optional)

Authentication can be enabled/disabled in the application.yml configuration file mentioned in [understanding configuration files](#understanding-configuration-files) section below. The default implementation uses Sunbird's authentication mechanism which is using keycloak for authentication. Keycloak installation details can be found [here](https://www.keycloak.org/docs/2.5/server_installation/topics/installation.html){:target="_blank"}. Authentication requires the below mentioned environment variables to be configured. Instructions to set up the SSO key can be found [here](https://www.keycloak.org/docs/3.1/server_admin/topics/realms/keys.html){:target="_blank"}.

```
sunbird_sso_publickey = ******
sunbird_sso_realm=sunbird
sunbird_sso_url=https://dev.open-sunbird.org/auth/
```

#### 2A: Out of the box = Teacher Registry
The default configuration files provided will be sufficient to start a registry instance. The default registry schema provided is for a Teacher registry.

#### 2B: Manual configuration (optional)
Edit the configuration files or create your own custom configuration files and configure the path. Read [understanding configuration files](#understanding-configuration-files) in the section below. If you just want to try it out, then skip this section and come back to it later.

* **Configuring custom configuration files**

	1. Read [understanding configuration files](#understanding-configuration-files) in the section below to create your own configuration files

	2. Add environment variables pointing to the configuration files.
```
	registry_config_dir=file://...
	config_schema_file=${registry_config_dir}schema-configuration.jsonld
	validations_create_file=${registry_config_dir}validations_create.shex
	validations_update_file=${registry_config_dir}validations_update.shex
	frame_file=${registry_config_dir}frame.json
	audit_frame_file=${registry_config_dir}audit_frame.json
```

#### 3 - Running the Registry

All dependencies are now installed. All required sample configuration files are also created and if you don't want to change anything, you may simply follow the following steps to start up an opensaber instance as a Teacher Registry.

##### Running using docker

In order to run using docker you need to install docker in your system. In the case of Linux systems, docker compose also needs to be installed.

```sh
cd registry
docker-compose up
```

##### Running it as a simple jar file

```sh
cd registry/target
java -jar registry.jar
```

#### 5 - Taking Registry for a spin!

##### Understanding Configuration Files

Below mentioned configuration files should be created in [src/main/resources](https://github.com/project-sunbird/open-saber/tree/master/java/registry/src/main/resources){:target="_blank"}. The script ```./configure-dependencies.sh``` will create the files to startup a full fledged Teacher Registry, but you can edit these files to suit your domain. The sample files contain comments which further explain each property.

1. **application.yml** - Create a YAML configuration file which contains various environment specific configurations for the application. The default profile will be **development** environment. The spring.profiles.active configuration needs to be changed to the environment where the application is deployed. Sample configuration details can be found in [application.yml.sample](https://github.com/project-sunbird/open-saber/blob/master/java/registry/src/main/resources/application.yml.sample){:target="_blank"}.

2. **validations_*.shex** - These file(s) should contain static and declarative validations. For further details on syntax, you can refer to the [Shape Expressions Primer(Shex Primer)](http://shex.io/shex-primer/){:target="_blank"}. Two separate files are required during creation and updation of entities. An example for the validations can be found in [validation_create.shex.sample](https://github.com/project-sunbird/open-saber/blob/master/java/registry/src/main/resources/validations_create.shex.sample){:target="_blank"}.

3. **schema-configuration.jsonlencryption_based** - This file should contain schema level configurations. Further details can be found in [schema-configuration.jsonld.sample](https://github.com/project-sunbird/open-saber/blob/master/java/registry/src/main/resources/schema-configuration.jsonld.sample){:target="_blank"}.
    
4. **frame.json** - This file is useful to frame the JSONLD output so that all the facts are nested instead of being flatly presented. This helps in readability. [frame.json.sample](https://github.com/project-sunbird/open-saber/blob/master/java/registry/src/main/resources/frame.json.sample){:target="_blank"} contains short-hand names, their namespaces and the the primary type used throughout the JSON-LD document that is issued into the registry.

5. **audit_frame.json** - If audit is enabled in application.yml, this file is useful to frame the audit records so that all the facts are nested instead of being flatly presented. This helps in readability. [audit_frame.json.sample](https://github.com/project-sunbird/open-saber/blob/master/java/registry/src/main/resources/audit_frame.json.sample){:target="_blank"} contains short-hand names, and their namespaces used throughout the audit record that is issued into the registry.


#### Property Configurations in Detail

The following is a list of configuration options which can be tailored for a specific instance of Opensaber. All these properties are environment variables and hence can be configured either in .bashrc or in Windows environment properties. Most of the properties have sensible defaults.

1. **perf_monitoring_enabled** - This property is used to enable/disable performance instrumentation to performance tune various APIs.

2. **registry_context_base** - The primary namespace IRI of the registry instance. It will default to `http://localhost:8080/`.

3. **registry_system_base** - The namespace IRI for audit records. This will default to `http://localhost:8080/opensaber`.

4. **config_schema_file** - The fully qualified filename with the `file://` protocol prefix for configuring fields that need to be encrypted. The default filename will be `schema-configuration.jsonld` and will be loaded from the classpath. This file will be in JSON-LD format.

5. **database_provider** - The storage database provider for the Opensaber instance. The default database will be `NEO4J`.

6. **database_embedded** - Set this property to `true` to enable running an embedded Neo4J instance with Opensaber.

7. **database_directory** - Set this property to a directory path if an embedded Neo4J instance is used.

8. **database_host** - The hostname or IP of the machine on which Neo4J database is running.

9. **database_port** - The port on which Neo4J database instance is running. It defaults to 7687 which is the default port for bolt protocol.

10. **validations_create_file** - The fully qualified filename with the `file://` protocol prefix for validating input data for the create API. The default value will be `validations_create.shex` and will be loaded from the classpath. For further details, you can refer to [understanding configuration files](#understanding-configuration-files) above.

12. **validations_update_file** - The fully qualified filename with the `file://` protocol prefix for validating input data for the update API. The default value will be `validations_update.shex` and will be loaded from the classpath. For further details, you can refer to [understanding configuration files](#understanding-configuration-files) above.

13. **frame_file** - The Full qualified filename with the `file://` protocol prefix for framing a record read from the database. The default value will be `frame.json` and will be loaded from the classpath. For further details, you can refer to [understanding configuration files](#understanding-configuration-files) above.

14. **connection_timeout** - Encryption service connection timeout in milliseconds.

15. **connection_request_timeout** - Encryption service connection request timeout in milliseconds.

16. **read_timeout** - Encryption service socket read timeout in milliseconds.

17. **encryption_enabled** - Toggle for enabling/disabling encryption.

18. **encryption_base** - The base URL for encryption/decryption service.

19. **encryption_uri** - The fully qualified URI for encrypting data.

20. **encryption_batch_uri** - The fully qualified URL to encrypt data in batch mode.

21. **decryption_uri** - The fully qualified URI for decrypting data.

22. **decryption_batch_uri** - The fully qualified URL to decrypt data in batch mode.

23. **audit_enabled** - Toggle to enable/disable internal audit. The audit records will be stored as part of the primary database.

24. **audit_frame_file** - The fully qualified filename with the `file://` protocol prefix for framing an audit record read from the database. The default value will be `audit_frame.json` and will be loaded from the classpath. For further details, you can refer to [understanding configuration files](#understanding-configuration-files) above.

25. **authentication_enabled** - Toggle to enable/disable authentication. The authentication is disabled by default. The default authentication provider is the Sunbird Keycloak service.

26. **sunbird_sso_publickey** - The public key of the Sunbird Keycloak authentication service.

27. **sunbird_sso_realm** - The SSO realm of the Sunbird Keycloak authentication service.

28. **sunbird_sso_url** - The fully qualified URL of the authentication service.


#### Understanding the Vocabulary File

Create a domain specific vocabulary file for the application. Sample vocabulary file can be found [vocabulary.owl.sample](https://github.com/project-sunbird/open-saber/tree/master/java/registry/src/main/resources/vocabulary/vocabulary.owl.sample){:target="_blank"}. This file should be placed in [src/main/resources/vocabulary](https://github.com/project-sunbird/open-saber/tree/master/java/registry/src/main/resources/vocabulary){:target="_blank"}, so that it can be served as a static resource. This is useful for machine readability of your registry and also helps in understanding various terms being used in the vocabulary.


#### Testing the APIs

[Open Saber API specs](/api-specs.html) and [Open Saber API Examples](/api-examples.html) give detailed descriptions on how to use the APIs in Registry.



