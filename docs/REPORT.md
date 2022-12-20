# Lab 6 report

## Architecture

## Registering services

> **Warning:** The registration service must be running before any registrations can be made. This can be done using the following command:
  
```bash
./gradlew registration:bootRun
```

To start we launch the `accounts (2222)` and `web` services.

- **`accounts`**
```bash
./gradlew accounts:bootRun
```

- **`web`**
```bash
./gradlew web:bootRun
```

In the following image we can see how both services are working correctly at the same time as the registration service.
- `TL (Top Left)` terminal: Account service
- `BL (Bottom Left)` terminal: Web service
- `R  (Right)` terminal: Registration service

![image](/docs/assets/logs-1.png)

### Registration service Proofs 

Below is an image showing the correct registration of the services.
![image](/docs/assets/proof-1.png)

## Adding a new service

Now, I proceed to add a new service `account (4444)`.  
To do this, the `port` property located at the following path has been modified: `accounts/src/main/resources/application.yml`

```bash	
./gradlew account:bootRun
```	

- `TL (Top Left)` terminal: `Account (2222)` service
- `TR  (Top Right)` terminal: `Account (1111)` service
- `BL (Bottom Left)` terminal: `Web (3333)` service
- `BR  (Bottom Right)` terminal: `Registration (4444)` service

![image](/docs/assets/logs-2.png)

### Registration service Proofs 

Below is an image showing the correct registration of the services.

![image](/docs/assets/proof-2.png)

In this one, we can see how there is one instance for the `WEB-SERVICE` application and two for the `ACCOUNTS-SERVICE` one.

![image](/docs/assets/proof-2.1.png)

 <!-- press control c to stop -->

## Shutting down a service

Now, I proceed to shut down the `account (2222)` service and see how the `web (3333)` service reacts.
For that, I have to press <kbd>ctrl + c</kbd> in the `account (2222)` terminal.

![image](/docs/assets/stop-1.png)

Now we can see how the `web (3333)` service has noticed that the `account (2222)` service has been stopped.

![image](/docs/assets/proof-3.png)

To check that the `web (3333)` service is working correctly, I accessed the following URL: `http://localhost:3333/accounts/123456789` and got the following response:

![image](/docs/assets/proof-4.png)

showing that the `web (3333)` service is working correctly because eureka has detected that the `account (2222)` service has stopped working and has redirected the request to the `account (1111)` service.