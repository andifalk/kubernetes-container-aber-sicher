# Default Docker Container

This demo builds a standard docker image from the demo application just using a standard _Dockerfile_.
For details on the demo application see [hello spring boot application](../step1-hello-spring-boot).

When using defaults for building a container image the container will run using
the root user by default.
  
You can prove this by using these commands:

```bash
docker container run --rm --detach --name hello-root \
-p 8080:8080 andifalk/hello-root:latest
docker exec hello-root whoami
```

This should return the following user information (it really is root)

```bash
root
```

You should also be able to reach the dockerized application 
via http://localhost:8080.

Finally stop the running container by using the following command:

```bash
docker stop hello-root
```

## Check image for Vulnerabilities

Now we can check our image for vulnerabilities with high and cxritical severities 
using this command:

```bash
trivy --clear-cache --severity HIGH,CRITICAL andifalk/hello-root:latest
```