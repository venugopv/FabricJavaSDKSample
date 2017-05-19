# Summary
________
The following example demonstrates the java sdk running a sample program against docker images of a working commit level of the Hyperledger Fabric V1.0 architecture.

It downloads Fabric Java SDK jar from Nexus repository(in future the jar will be pulled from maven repository. The jar will be uploaded to maven repository by **Hyperledger fabric-sdk-java** project)

The sample runs two end to end test cases. These two test cases are primarly taken from [Hyperledger fabric-sdk-java](https://github.com/hyperledger/fabric-sdk-java) tests.
### 1)End2endTest
  * Creates two chains (chain 'foo for org1'and chain 'bar' for org2) with each having two peers(peer1 and peer2)
  * Then it installs (and then instantaites) a balance transfer chaincode on chains.
  * Upon successful instantiation of chain code, it does a balnace transfer from 'a' to 'b' by invoking chaincode.
  * It does Query of chaincode to validate previous invoke.
  * It travereses blocks through chain and displays them to console.
### 2)End2endUpdateCCTest
This test runs on top of **End2endTest**. It upgrades chaincode and validates the same.
  * Creates two chains (chain 'foo for org1'and chain 'bar' for org2) with each having two peers(peer1 and peer2)
  * Validates values of 'a' and 'b' by calling Query on chaincode.
  * chaincode is upgraded and validations is done to verify ledger data is persisted or not.
  * Perform invoke() and validate.

## Prerequisites
___
To build this project, following dependencies must be met
  * JDK 1.8 or above
  * Apache Maven
  * Docker - v1.12 or higher
  * Docker Compose - v1.8 or higher 

## How to run sample tests
___ 

# Step 1 : Clone the sample git repository or extract the zip file
The sample proejct contains:
    * src/test/java - two unit test source files.
    * src/test/fixture: artifacts required for test.
      
      `cd src/test/fixture/sdkintegration` 
      `./fabric.sh clean`
      This would clean any previous docker containers if they are any.
      
      Run the docker-compose file that will pull the docker images and start fabric
      'docker-compose up -d'
      (run 'docker-compose down' to stop fabric and remove fabric docker containers)
      
# Step 2: Run sample tests.
    'cd ../../../../'
    (this is sample project home directory i.e pom.xml should be present)
    
    Now run 'mvn package'.
    'mvn package'
    This would download Fabric Java SDK jar from maven repository and then builds and runs the two test cases. You should see tests output on console.

# Configuration
* Few properties can be configured in test/java/org/hyperledger/fabric/sdk/testutils.properties.
* src/test/java/org/hyperledger/fabric/sdk/testutils/TestConfig.java: Reads config from testutils.properties and defaults parameters which are not configured.
* chaincode endorsement policies can be configured by modifying YAML files in src/test/fixture/sample_chaincode_endorsement_policies 

# Chaincode
Version 1 Balance transfer chaincode: src/test/fixture/sdkintegration/gocc/sample1/src/github.com/example_cc/example_cc.go

Version 11 Balance trransfer chaincdoe (this chaincode is updated in End2endUpdateCCTest test): src/test/fixture/sdkintegration/gocc/sample_11/src/github.com/example_cc/example_cc.go




    
    
    
    