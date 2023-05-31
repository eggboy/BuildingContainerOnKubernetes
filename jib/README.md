# Jib

1. What is it and Why use it?
   Here is the introduction according to the official repository.
   "Jib builds optimized Docker and OCI images for your Java applications without a Docker daemon - and without deep
   mastery of Docker best-practices. It is available as plugins for Maven and Gradle and as a Java library."
   Plugins for Maven and Gradle are the best advantage for Java developers to consider Jib. It's basically an Java
   library which doesn't require a Docker daemon locally, and building container can be part of maven lifecycle which
   makes CI process much easier.

2. How to use it
   Best way to use it is to configure it with pom.xml. You can find the extensive list
   of options here. 

```xml
  <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
            <plugin>
                <groupId>com.google.cloud.tools</groupId>
                <artifactId>jib-maven-plugin</artifactId>
                <version>3.3.2</version>
                <configuration>
                    <from>
                        <image>mcr.microsoft.com/openjdk/jdk:17-ubuntu</image>
                    </from>
                    <to>
                        <image>${env.IMAGE}</image>
                    </to>
                    <container>
                        <jvmFlags>
                            <jvmFlag>-Xms512m</jvmFlag>
                            <jvmFlag>-Xmx512m</jvmFlag>
                            <jvmFlag>-Xdebug</jvmFlag>
                        </jvmFlags>
                    </container>
                </configuration>
            </plugin>
        </plugins>
    </build>
...
```
3.Then use it with maven.
```bash
$ export IMAGE=eggboy/jib:0.0.1
$ mvn jib:build
```