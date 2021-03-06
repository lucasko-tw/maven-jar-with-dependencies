Using Maven makes Jar file with dependencies
==================================

[Maven in 5 Minutes](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)


### Edit pom.xml from Maven Project

Import dependency into project.

```xml
	<dependencies>

		<dependency>
			<groupId>log4j</groupId>
			<artifactId>log4j</artifactId>
			<version>1.2.17</version>
		</dependency>

	</dependencies>
```


Maven Assembly Plugin

```xml
<build>
		<finalName>${project.artifactId}</finalName>
		<plugins>
		
			<!-- download source code in Eclipse, best practice -->
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-eclipse-plugin</artifactId>
				<version>2.9</version>
				<configuration>
					<downloadSources>true</downloadSources>
					<downloadJavadocs>false</downloadJavadocs>
				</configuration>
			</plugin>


			<!-- Set a compiler level -->
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-compiler-plugin</artifactId>
				<version>2.3.2</version>
				<configuration>
					<source>1.8</source>
					<target>1.8</target>
				</configuration>
			</plugin>

			<!-- Maven Assembly Plugin -->
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-assembly-plugin</artifactId>
				<version>2.4.1</version>
				<configuration>
					<!-- get all project dependencies -->
					<descriptorRefs>
						<descriptorRef>jar-with-dependencies</descriptorRef>
					</descriptorRefs>
					<!-- MainClass in mainfest make a executable jar -->
					<archive>
						<manifest>
							<mainClass>org.lucasko.App</mainClass>
						</manifest>
					</archive>

				</configuration>
				<executions>
					<execution>
						<id>make-assembly</id>
						<!-- bind to the packaging phase -->
						<phase>package</phase>
						<goals>
							<goal>single</goal>
						</goals>
					</execution>
				</executions>
			</plugin>
		</plugins>
	</build>
```


### App.java

```JAVA
package org.lucasko;

import org.apache.log4j.Logger;

public class App {

	public static Logger logger = Logger.getLogger(App.class);
	
	public static void main(String[] args)  {
		
		logger.info("Hello World");
		
	}

}
```

![App.java](https://github.com/lucasko-tw/maven-jar-with-dependencies/blob/master/jar-with-dependencies.png)


### Create jar file

compile: compile the source code of the project
 
```sh
 mvn compile
```

package: take the compiled code and package it in its distributable format, such as a JAR.

```sh
 mvn package
```
the jar is created in target/tutorial-maven-jar-with-dependencies.jar

### Run jar file

```sh
  java -jar tutorial-maven-jar-with-dependencies.jar
```

the result is:

	[16/11/19 09:48:12][INFO][org.lucasko.App-11] Hello World


