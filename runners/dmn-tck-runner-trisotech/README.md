# DMN TCK Trisotech Runner

This runner differs a little bit from the other runners available in this repository in the sense that the test cases are not executed locally but are executed on a Trisotech DMN Digital Cloud Execution through its http/https REST API.

It requires an extra configuration file that needs to be located under the user home directory in a file named .dmn-tck-runner-trisotech.properties.

```
  url=https://xxx.trisotech.com

  bearer=xxx

  repo=tck
```

###### url
The URL of the Trisotech Digital Enterprise Suite on which the Trisotech DMN Digital Cloud Execution is activated.

###### bearer
A REST API bearer token for OAUTH authentication with the DMN Digital Cloud Execution. This can be generated by going to the Trisotech DES Admin (url/admin) and creating a new Client App with the grants for Execution Repository Read/Write and DMN Execution. If you don't see those claims when creating a Client App, it means that you don't have the Trisotech DMN Digital Cloud Execution activated in your current DES license.

Once the Client App generated, click on the generate token button to get your token.

###### repo
The name of an Execution Repository to which you have Read/Write access. Execution Repository can also be created by going to the Trisotech DES Admin (url/admin). Make sure that you have given access to the user that will generate the bearer token.


## Using the Trisotech DMN TCK Runner

The Trisotech DMN TCK Runner comes in two flavor:

- As jUnit 4 tests
- As a command line tool

Both are quite useful and only depends if you prefer IDE integration or cute colors.

###### Maven integration

```
$ mvn clean install
```

This will build and run the unit tests based on your property file configuration. After execution, a file name *tck_results.csv* is automatically generated in the target directory. This file respects the submission format of the TCK.

###### Command line executable jar

```
$ mvn -DskipTests clean install
```

This will build an executable jar skipping the test integration with jUnit. The executable jar will be called tck-runner-trisotech-[version].one-jar in your target subdirectory.

You can then use this jar to run the tests using the console

```
java -jar tck-runner-trisotech-[version].one-jar [TCK Test Cases folder]
```

If unspecified, the current working directory will be considered the TCK Test Case folder.


###### To build automatically this runner when building the parent project

In the parent project, create an enable-trisotech.flag file

```
$ touch enable-trisotech.flag
```