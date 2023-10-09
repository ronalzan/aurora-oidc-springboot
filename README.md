# Spring Boot, OIDC, and Aurora

A Spring Boot example app that shows how to implement single sign-on (SSO) with OpenID Connect (OIDC) and Aurora.

**Prerequisites:** 

- Java 8
- Spring Tools
- Maven

### Getting Started

1) To install this example application, run the following commands:

```bash
git clone https://github.com/ronalzan/aurora-oidc-springboot.git
cd aurora-oidc-springboot
```

2) Import as maven project

### Register Application

Aurora developer is responsible for this step.

### Import the Aurora certificate

1. Aurora support provide the certificate

2. Locate $JAVA_HOME/jre/lib/security/cacerts

3. Import the certificate into the cacerts file using the following:

```shell
keytool -import -alias auroraCertificate -keystore cacerts -file <AURORA_CERTIFICATE_FILE_LOCATION>
```
                        
### Application Configuration
  
- Open the `application.yml` file located in `oidc-spring-boot-sample/src/main/resources`.
  
- Update the following configuration. 
  
```yaml

provider:
  host: <server-host-name> #Aurora support to provide

client:
  client-id: <application-client-id> #Aurora support to provide
  client-secret: <application-client-secret> #Aurora support to provide
  post-logout-uri: http://localhost:8080/login
  scope: openid
  authorization-grant-type: authorization_code

spring:
  security:
    oauth2:
      client:
        registration:
          wso2:
            client-name : Aurora
            client-id: <application-client-id> #Aurora support to provide
            client-secret: <application-client-secret> #Aurora support to provide
            authorization-grant-type: authorization_code
            scope: openid
        provider:
          wso2:
            issuer-uri: <aurora issuer> #Aurora support to provide
 
```

### Build the sample and Run it
  
  - Run `mvn clean install`. 
  - Access `http://localhost:8080` 
