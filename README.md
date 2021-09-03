# Implement a BPMN Parallel Gateway in Camunda
The article contains a step-by-step guide on how to implement a BPMN Parallel Gateway in Camunda making use of a Spring Boot Application. 

**Java Nibble Article:** [https://www.javanibble.com/implement-bpmn-parallel-gateway-in-camunda/](https://www.javanibble.com/implement-bpmn-parallel-gateway-in-camunda/)

## Pre-Requisites
The following is required to run the Spring Boot example:
* [curl](https://www.javanibble.com/how-to-install-curl-on-macos-using-homebrew/)
* jq
* [maven](https://www.javanibble.com/how-to-install-maven-on-macos-using-homebrew/)

## BPMN Parallel Gateway
A Parallel Gateway creates parallel paths without checking any conditions; each outgoing Sequence Flow receives a token upon execution of this Gateway. For incoming flows, the Parallel Gateway will wait for all incoming flows before triggering the flow through its outgoing Sequence Flows.

Use Camunda Modeller to model the process. The process model is composed of five tasks and two parallel gateways:

![BPMN Parallel Gateway](https://www.javanibble.com/assets/images/posts/bpmn-parallel-gateway/camunda-bpmn-parallel-gateway.png)

* Retrieve Coffee Order: Is a `Service Task` linked to a Delegate Expressions with the name `${logger}`.
* Make Coffee: Is a `Service Task` linked to a Delegate Expressions with the name `${logger}`.
* Retrieve Cup & Saucer: Is a `Service Task` linked to a Delegate Expressions with the name `${logger}`.
* Pour Coffee in Cup: Is a `Service Task` linked to a Delegate Expressions with the name `${logger}`.
* Deliver Coffee Order:Is a `Service Task` linked to a Delegate Expressions with the name `${logger}`.


## Compile & Run The Example
### 1. Compile the application
Use the following command to compile the Spring Boot application making use of maven:

```shell
$ mvn clean install
```

### 2. Run the application
After you have successfully built the Camunda BPM Spring Boot application, the compiled artifact can be found in the
target directory. Use the following command to start the Camunda BPM Spring Boot Application.

```shell
$ maven spring-boot:run
```

### 3. Execute the example
After the application has started, run the following command in another terminal:

**Run the command: Start Process Instance**

The following command instantiates a new instance of the `order-coffee` process.

```shell
$ ./start_process_scenario_01.sh
```
The script performs the following commands:
```shell
curl --location --request POST 'http://localhost:8080/engine-rest/process-definition/key/order-coffee/start' --header 'Content-Type: application/json'
```
The following is the output to the console after running the above command.

![Console](https://www.javanibble.com/assets/images/posts/bpmn-parallel-gateway/console-camunda-bpmn-parallel-gateway.png)


## View Camunda Admin Console
To view the Camunda Admin Console, type the following url in your browser while the application is running. You will be prompted with the login screen.

* [http://localhost:8080/](http://localhost:8080/)

After you have typed the above URL in a browser while the application is running, you will be prompted with the login screen. Type the Username and Password you set within the application properties file.


## View the H2 Console
To view the H2 Console, type the following url in your browser while the application is running. You will be prompted with the login screen.

* [http://localhost:8080/h2-console](http://localhost:8080/h2-console)

After you have typed the above URL in a browser while the application is running, you will be prompted with the login screen. Press the connect button since there is no password specified.
