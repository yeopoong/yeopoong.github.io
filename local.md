개발환경
=======

Nexus 
-----

Private library repository 를 사용하기 위해서 Nexus를 설정한다.

### Maven repository 설정
Nexus 서버의 접근권한을 설정하기 위해서 maven 설정파일인 setting.xml에 다음의 내용을 추가한다.

```
<servers>
...
    <server>
      <id>releases</id>
      <username>deployment</username>
      <password>deployment123</password>
    </server>  
    <server>
      <id>snapshots</id>
      <username>deployment</username>
      <password>deployment123</password>
    </server>  
    <server>
      <id>thirdparty</id>
      <username>deployment</username>
      <password>deployment123</password>
    </server>
...
</servers>
```

Maven Central 레포지토리 대신에 Nexus 서버를 프록시 서버로 사용하도록 다음의 설정을 pom.xml 에 추가한다.

```
    <repositories>
      <repository>
        <id>central</id>
        <url>http://192.168.0.115:8080/nexus/content/groups/public</url>
        <releases><enabled>true</enabled></releases>
        <snapshots><enabled>true</enabled></snapshots>
      </repository>
    </repositories>

    <pluginRepositories>
      <pluginRepository>
        <id>central</id>
        <url>http://192.168.0.115:8080/nexus/content/groups/public</url>
        <releases><enabled>true</enabled></releases>
        <snapshots><enabled>true</enabled></snapshots>
      </pluginRepository>
    </pluginRepositories>
```

어플리케이션의 배포본을 Nexus Snapshots 레포지토리에 배포하기 위해서 다음의 설정을 pom.xml 에 추가한다.

```
    <distributionManagement>
        <repository>
            <id>releases</id>
            <url>http://192.168.0.115:8080/nexus/content/repositories/releases</url>
        </repository>
        <snapshotRepository>
            <id>snapshots</id>
            <url>http://192.168.0.115:8080/nexus/content/repositories/snapshots</url>
        </snapshotRepository>
    </distributionManagement>
```

Maven Release
-------------

다음과 같이 pom.xml 에 Maven Release Plugin 과 scm 설정을 추가한다.

```
  <scm>
        <connection>scm:git:https://github.com/t3qdev/nextg.git</connection>
        <url>http://github.com/t3qdev/nextg</url>
        <developerConnection>scm:git:https://github.com/t3qdev/nextg.git</developerConnection>
  </scm>
```


```
  <scm>
        <connection>scm:git:https://github.com/t3qdev/nextg.git</connection>
        <url>http://github.com/t3qdev/nextg</url>
        <developerConnection>scm:git:https://github.com/t3qdev/nextg.git</developerConnection>
  </scm>
```

```
    <build>
        <plugins>
            ....
            <plugin>
                <artifactId>maven-release-plugin</artifactId>
                <version>2.5.3</version>
                <configuration>
                    <autoVersionSubmodules>true</autoVersionSubmodules>
                    <goals>deploy</goals>
                    <arguments>-Dmaven.javadoc.skip=true</arguments>
                </configuration>
                <dependencies>
                    <dependency>
                        <groupId>org.apache.maven.shared</groupId>
                        <artifactId>maven-invoker</artifactId>
                        <version>2.2</version>
                    </dependency>
                </dependencies>
            </plugin>
            ...
        </plugins>
    </build>
```
  
