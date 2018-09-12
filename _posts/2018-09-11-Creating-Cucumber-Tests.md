---
date: 2018-09-10
title: Create Cucumber tests
categories:
  - Documentation
type: Document
showSidebar: false
published: false
nav_ordering: 12
pageTitle: "Create Cucumber tests"
---
## STEPS TO CREATE CUCUMBER TESTS

1. Create a [feature](https://docs.cucumber.io/gherkin/reference/#feature){:target="_blank"} file with the below information.
   * A line starting with the keyword **Feature** followed by a statement indicating the purpose of the test
   * Multiple scenarios which are also statements starting with the keyword **Scenario** followed by a line specifying the scenario or different scenarios for the test
   * Under each scenario statement, steps are created using the keywords [Given, When and Then](https://docs.cucumber.io/gherkin/reference/#steps){:target="_blank"}
        * Given - Statements beginning with the keyword **Given**, and used to specify test assumptions or                    validations
        * When -  Statements beginning with the keyword **When**, and used to specify the key action that the 
scenario achieves
        * Then - Statements beginning with the keyword **Then**, and used to specify the outcome of the scenario

2. Create a java class in which the features, scenarios and steps mentioned above are implemented. An example can be found [here](https://github.com/project-sunbird/open-saber/blob/master/java/cukes/src/test/java/io/opensaber/registry/test/RegistryIntegrationSteps.java){:target="_blank"}.

3. Create a test class with a sample format as given below. The keyword **features** is used to specify paths of .feature files and **glue** keyword is used to specify paths of steps files. 

```
@RunWith(Cucumber.class)
@CucumberOptions(features = "", glue = {""})
public class SampleTest {

}
```

4. When this test class is executed, it picks up the feature files and classes which contains the steps implementation based on the path specified and executes them.
