# Initial Spring Boot Application

This is the initial demo application that will be used for showing
all security patterns when deploying and running this in Kubernetes.

This application provides two REST APIs:

* Greetings API
  * GET [localhost:8080](http://localhost:8080): Shows greeting with configured default message
  * GET [localhost:8080?message=test](http://localhost:8080?message=test): Shows greeting with custom message
* Actuator API
  * Exposes all available [actuator endpoints](http://localhost:8080/actuator) of Spring Boot (including sensitive ones)

The application is kept simple to focus on the security parts instead of having to describe
a complex use case model.
    
## Run the application

Just start it by running _com.example.app.Step1App_.

## Sample command client requests

### Httpie

This should return the default greeting:

```bash
http localhost:8080
```

This should return a custom greeting:

```bash
http localhost:8080 "message==Test"
```

### Curl

This should return the default greeting:

```bash
curl http://localhost:8080
```

This should return a custom greeting:

```bash
curl http://localhost:8080\?message\=Test
```

## Sample browser requests

By using the browser we can try to put in 
some cross-site scripting (XSS) snippets into the message parameter.

Try to display a popup via javascript:

```http request
http://localhost:8080/?message=<script>alert('XSS')</script>
```

Try to redirect to Google search via XSS:

```http request
http://localhost:8080/?message=<script>document.location="http://www.google.com/"</script>
``` 

With the default code XSS is not working as there are multiple 
defense mechanisms in place:

* Input validation only permits maximum length of _30_ for url message parameter
* The application is safe against interpreting the reflected greeting by using output escaping (Html AND javascript)
* Content-Type is set to _application/json_ 

Note:  
If you disable all these precautions then you should see XSS working.
Please do __not disable__ those precautions in productive code !!! 

## Build process

The gradle build for this application includes specific security relevant parts:

* SpotBugs (with Security Add-On): Automatically does static code analysis for security issues
* OWASP Dependency Check: Automatically checks all gradle dependencies for known vulnerabilities

## Next

[Next: Default Container](../step2-hello-root)
