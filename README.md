# tool.swagger.docgen

Swaggerdocgen Maven Plug-in provides a tool for generating Swagger documents for you web applications. The Swaggerdocgen Maven Plug-in 1.0 release is available on the [Maven central] (http://search.maven.org/#search%7Cga%7C1%7Cswaggerdocgen) repository. Alternatively, you can refer to [Installation] (#installation) section and follow the steps to install the plug-in in your local repository.

*Note:* When using the swaggerdocgen: goals, it is assumed that the package phase is already done. The Plugin is not responsible for packaging the web application into WAR.

## Installation

Use Maven 3.x to build the Swaggerdocgen plug-in.

1. Clone the repository
   ```sh
   $ git clone https://github.com/WASdev/tool.swagger.docgen.git
   ```

2. Navigate to the tool.swagger.docgen folder
   ```sh
   $ cd tool.swagger.docgen
   ```

3. Build the plug-in
   ```sh
   $ mvn install
   ```


## Plugin

### swaggerdocgen-maven-plugin

`swaggerdocgen-maven-plugin` can be used to extract the Swagger document from an application and merge it with any annotated endpoint data to create a unified Swagger document for the application.

#### Configuration

To enable `swaggerdocgen-maven-plugin` in your project add the following to your `pom.xml`:

```xml
<project>
    ...
    <build>
        <plugins>
            <!-- Enable liberty-maven-plugin -->
            <plugin>
                <groupId>net.wasdev.maven.plugins</groupId>
                <artifactId>swaggerdocgen-maven-plugin</artifactId>
                <version>1.0</version>
                <!-- Specify configuration, executions for swaggerdocgen-maven-plugin -->
                ...
            </plugin>

        </plugins>
    </build>
    ...
</project>
```

#### Goals

##### create
Creates a Swagger document for the web application. It can generate both YAML and JSON document depending on the **outputFile** parameter extension. If a Swagger document already exists in the WAR's META-INF/swagger.json or META-INF/swagger.yaml, it just converts the document to the right output format. 

Otherwise, it looks for META-INF/stub/swagger.json or META-INF/stub/swagger.yaml and also scans the application for Swagger/JAX-RS annotations, merging the data extracted from the stub document (if one exists) and annotations to generate a unified Swagger document.

Parameters used by this goal:

| Parameter | Description | Required |
| --------  | ----------- | -------  |
| outputFile | Location of the generated Swagger document. **Default value:** \${project.build.directory}/swagger.yaml | No |
| warFile| Location of the WAR to be scanned. **Default value:** \${project.build.directory}/\${project.build.finalName}.war | No |

Example:
```xml
<project>
    ...
    <build>
        <plugins>
            <plugin>
                <groupId>net.wasdev.maven.plugins</groupId>
                <artifactId>swaggerdocgen-maven-plugin</artifactId>
                <version>1.0</version>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>create</goal>
                        </goals>
                    </execution>
                </executions>
                <configuration>
                    <outputFile>${project.build.directory}/swagger.json</outputFile>
                </configuration>
            </plugin>
        </plugins>
    </build>
    ...
</project>
```

