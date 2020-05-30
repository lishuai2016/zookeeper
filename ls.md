当前代码基于版本tag3.6.0


# 1、源码构建

直接Git clone下来后执行clean install -Dmaven.test.skip=true或者clean package -Dmaven.test.skip=true即可





# 遇到的问题

1、运行主类QuorumPeerMain异常Caused by: java.lang.ClassNotFoundException: com.codahale.metrics.Reservoir

```java
D:\soft-install\jdk8\bin\java "-javaagent:D:\idea-2017-new\IntelliJ IDEA 2017.2.2\lib\idea_rt.jar=55969:D:\idea-2017-new\IntelliJ IDEA 2017.2.2\bin" -Dfile.encoding=UTF-8 -classpath D:\soft-install\jdk8\jre\lib\charsets.jar;D:\soft-install\jdk8\jre\lib\deploy.jar;D:\soft-install\jdk8\jre\lib\ext\access-bridge-64.jar;D:\soft-install\jdk8\jre\lib\ext\cldrdata.jar;D:\soft-install\jdk8\jre\lib\ext\dnsns.jar;D:\soft-install\jdk8\jre\lib\ext\jaccess.jar;D:\soft-install\jdk8\jre\lib\ext\jfxrt.jar;D:\soft-install\jdk8\jre\lib\ext\localedata.jar;D:\soft-install\jdk8\jre\lib\ext\nashorn.jar;D:\soft-install\jdk8\jre\lib\ext\sunec.jar;D:\soft-install\jdk8\jre\lib\ext\sunjce_provider.jar;D:\soft-install\jdk8\jre\lib\ext\sunmscapi.jar;D:\soft-install\jdk8\jre\lib\ext\sunpkcs11.jar;D:\soft-install\jdk8\jre\lib\ext\zipfs.jar;D:\soft-install\jdk8\jre\lib\javaws.jar;D:\soft-install\jdk8\jre\lib\jce.jar;D:\soft-install\jdk8\jre\lib\jfr.jar;D:\soft-install\jdk8\jre\lib\jfxswt.jar;D:\soft-install\jdk8\jre\lib\jsse.jar;D:\soft-install\jdk8\jre\lib\management-agent.jar;D:\soft-install\jdk8\jre\lib\plugin.jar;D:\soft-install\jdk8\jre\lib\resources.jar;D:\soft-install\jdk8\jre\lib\rt.jar;D:\opencode\zookeeper\zookeeper-server\target\classes;D:\maven-respo\commons-lang\commons-lang\2.6\commons-lang-2.6.jar;D:\opencode\zookeeper\zookeeper-jute\target\classes;D:\maven-respo\org\apache\yetus\audience-annotations\0.5.0\audience-annotations-0.5.0.jar;D:\maven-respo\io\netty\netty-handler\4.1.48.Final\netty-handler-4.1.48.Final.jar;D:\maven-respo\io\netty\netty-common\4.1.48.Final\netty-common-4.1.48.Final.jar;D:\maven-respo\io\netty\netty-resolver\4.1.48.Final\netty-resolver-4.1.48.Final.jar;D:\maven-respo\io\netty\netty-buffer\4.1.48.Final\netty-buffer-4.1.48.Final.jar;D:\maven-respo\io\netty\netty-transport\4.1.48.Final\netty-transport-4.1.48.Final.jar;D:\maven-respo\io\netty\netty-codec\4.1.48.Final\netty-codec-4.1.48.Final.jar;D:\maven-respo\io\netty\netty-transport-native-epoll\4.1.48.Final\netty-transport-native-epoll-4.1.48.Final.jar;D:\maven-respo\io\netty\netty-transport-native-unix-common\4.1.48.Final\netty-transport-native-unix-common-4.1.48.Final.jar;D:\maven-respo\org\slf4j\slf4j-api\1.7.25\slf4j-api-1.7.25.jar;D:\maven-respo\org\slf4j\slf4j-log4j12\1.7.25\slf4j-log4j12-1.7.25.jar;D:\maven-respo\log4j\log4j\1.2.17\log4j-1.2.17.jar org.apache.zookeeper.server.quorum.QuorumPeerMain conf/zoo.cfg
log4j:WARN No appenders could be found for logger (org.apache.zookeeper.server.quorum.QuorumPeerConfig).
log4j:WARN Please initialize the log4j system properly.
log4j:WARN See http://logging.apache.org/log4j/1.2/faq.html#noconfig for more info.
Exception in thread "main" java.lang.NoClassDefFoundError: com/codahale/metrics/Reservoir
	at org.apache.zookeeper.metrics.impl.DefaultMetricsProvider$DefaultMetricsContext.lambda$getSummary$2(DefaultMetricsProvider.java:126)
	at java.util.concurrent.ConcurrentHashMap.computeIfAbsent(ConcurrentHashMap.java:1660)
	at org.apache.zookeeper.metrics.impl.DefaultMetricsProvider$DefaultMetricsContext.getSummary(DefaultMetricsProvider.java:122)
	at org.apache.zookeeper.server.ServerMetrics.<init>(ServerMetrics.java:74)
	at org.apache.zookeeper.server.ServerMetrics.<clinit>(ServerMetrics.java:44)
	at org.apache.zookeeper.server.ZooKeeperServerMain.runFromConfig(ZooKeeperServerMain.java:132)
	at org.apache.zookeeper.server.ZooKeeperServerMain.initializeAndRun(ZooKeeperServerMain.java:112)
	at org.apache.zookeeper.server.ZooKeeperServerMain.main(ZooKeeperServerMain.java:67)
	at org.apache.zookeeper.server.quorum.QuorumPeerMain.initializeAndRun(QuorumPeerMain.java:140)
	at org.apache.zookeeper.server.quorum.QuorumPeerMain.main(QuorumPeerMain.java:90)
Caused by: java.lang.ClassNotFoundException: com.codahale.metrics.Reservoir
	at java.net.URLClassLoader.findClass(URLClassLoader.java:381)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:424)
	at sun.misc.Launcher$AppClassLoader.loadClass(Launcher.java:349)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:357)
	... 10 more

Process finished with exit code 1

```


解决思路：因为有些类引入是provided，把相关的provided去掉就行了

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <!--
  /**
   * Licensed to the Apache Software Foundation (ASF) under one
   * or more contributor license agreements.  See the NOTICE file
   * distributed with this work for additional information
   * regarding copyright ownership.  The ASF licenses this file
   * to you under the Apache License, Version 2.0 (the
   * "License"); you may not use this file except in compliance
   * with the License.  You may obtain a copy of the License at
   *
   *     http://www.apache.org/licenses/LICENSE-2.0
   *
   * Unless required by applicable law or agreed to in writing, software
   * distributed under the License is distributed on an "AS IS" BASIS,
   * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   * See the License for the specific language governing permissions and
   * limitations under the License.
   */
  -->
  <modelVersion>4.0.0</modelVersion>
  <parent>
    <groupId>org.apache.zookeeper</groupId>
    <artifactId>parent</artifactId>
    <version>3.6.0</version>
    <relativePath>..</relativePath>
  </parent>

  <groupId>org.apache.zookeeper</groupId>
  <artifactId>zookeeper</artifactId>
  <packaging>jar</packaging>
  <name>Apache ZooKeeper - Server</name>
  <description>ZooKeeper server</description>

  <dependencies>
    <dependency>
      <groupId>com.github.spotbugs</groupId>
      <artifactId>spotbugs-annotations</artifactId>
      <scope>provided</scope>
      <optional>true</optional>
    </dependency>
    <dependency>
      <groupId>org.hamcrest</groupId>
      <artifactId>hamcrest-all</artifactId>
      <scope>test</scope>
    </dependency>
    <dependency>
      <groupId>commons-collections</groupId>
      <artifactId>commons-collections</artifactId>
      <scope>test</scope>
    </dependency>
    <dependency>
      <groupId>commons-lang</groupId>
      <artifactId>commons-lang</artifactId>
    </dependency>
    <dependency>
      <groupId>org.apache.zookeeper</groupId>
      <artifactId>zookeeper-jute</artifactId>
      <version>${project.version}</version>
    </dependency>
    <dependency>
      <groupId>commons-cli</groupId>
      <artifactId>commons-cli</artifactId>
      <scope>provided</scope>
    </dependency>
    <dependency>
      <groupId>org.apache.yetus</groupId>
      <artifactId>audience-annotations</artifactId>
    </dependency>
    <dependency>
      <groupId>io.netty</groupId>
      <artifactId>netty-handler</artifactId>
    </dependency>
    <dependency>
      <groupId>io.netty</groupId>
      <artifactId>netty-transport-native-epoll</artifactId>
    </dependency>
    <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-api</artifactId>
    </dependency>
    <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-log4j12</artifactId>
    </dependency>
    <dependency>
      <groupId>org.eclipse.jetty</groupId>
      <artifactId>jetty-server</artifactId>
      <!--<scope>provided</scope>-->
    </dependency>
    <dependency>
      <groupId>org.eclipse.jetty</groupId>
      <artifactId>jetty-servlet</artifactId>
      <!--<scope>provided</scope>-->
    </dependency>
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-databind</artifactId>
      <!--<scope>provided</scope>-->
    </dependency>
    <dependency>
      <groupId>com.googlecode.json-simple</groupId>
      <artifactId>json-simple</artifactId>
      <!--<scope>provided</scope>-->
    </dependency>
    <dependency>
      <groupId>org.bouncycastle</groupId>
      <artifactId>bcprov-jdk15on</artifactId>
      <scope>test</scope>
    </dependency>
    <dependency>
      <groupId>org.bouncycastle</groupId>
      <artifactId>bcpkix-jdk15on</artifactId>
      <scope>test</scope>
    </dependency>
    <dependency>
      <groupId>jline</groupId>
      <artifactId>jline</artifactId>
      <scope>provided</scope>
    </dependency>
    <dependency>
       <groupId>io.dropwizard.metrics</groupId>
       <artifactId>metrics-core</artifactId>
       <!--<scope>provided</scope>-->
    </dependency>
    <dependency>
      <groupId>log4j</groupId>
      <artifactId>log4j</artifactId>
    </dependency>
    <dependency>
      <groupId>org.apache.kerby</groupId>
      <artifactId>kerb-core</artifactId>
      <scope>test</scope>
    </dependency>
    <dependency>
      <groupId>org.apache.kerby</groupId>
      <artifactId>kerb-simplekdc</artifactId>
      <scope>test</scope>
    </dependency>
    <dependency>
      <groupId>org.apache.kerby</groupId>
      <artifactId>kerby-config</artifactId>
      <scope>test</scope>
    </dependency>
    <dependency>
      <groupId>org.mockito</groupId>
      <artifactId>mockito-core</artifactId>
      <scope>test</scope>
    </dependency>
    <dependency>
      <groupId>org.jmockit</groupId>
      <artifactId>jmockit</artifactId>
      <scope>test</scope>
    </dependency>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <scope>test</scope>
    </dependency>
    <dependency>
      <groupId>org.xerial.snappy</groupId>
      <artifactId>snappy-java</artifactId>
      <!--<scope>provided</scope>-->
    </dependency>
  </dependencies>

  <build>
    <plugins>
      <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>properties-maven-plugin</artifactId>
        <executions>
          <execution>
            <phase>initialize</phase>
            <goals>
              <goal>read-project-properties</goal>
            </goals>
            <configuration>
              <files>
                <file>${basedir}/src/main/resources/git.properties</file>
              </files>
            </configuration>
          </execution>
        </executions>
      </plugin>
      <plugin> <!-- ${maven.build.timestamp} does not support timezone :( -->
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>build-helper-maven-plugin</artifactId>
        <executions>
          <execution>
            <id>tbuild-time</id>
            <goals>
              <goal>timestamp-property</goal>
            </goals>
            <configuration>
              <name>build.time</name>
              <pattern>MM/dd/yyyy HH:mm zz</pattern>
              <locale>en_US</locale>
              <timeZone>GMT</timeZone>
            </configuration>
          </execution>
          <execution>
            <phase>generate-sources</phase>
            <goals>
              <goal>add-source</goal>
            </goals>
            <configuration>
              <sources>
                <source>${project.build.directory}/generated-sources/java</source>
              </sources>
            </configuration>
          </execution>
        </executions>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <executions>
          <execution>
            <id>pre-compile-vergen</id>
            <phase>generate-sources</phase>
            <configuration>
              <includes>
                <include>org/apache/zookeeper/version/**/*.java</include>
              </includes>
            </configuration>
            <goals>
              <goal>compile</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
      <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>exec-maven-plugin</artifactId>
        <executions>
          <execution>
            <id>generate-version-info</id>
            <phase>generate-sources</phase>
            <goals>
              <goal>exec</goal>
            </goals>
            <configuration>
              <workingDirectory>${project.basedir}/src/main/java/</workingDirectory>
              <executable>java</executable>
              <arguments>
                <argument>-classpath</argument>
                <classpath />
                <argument>org.apache.zookeeper.version.util.VerGen</argument>
                <argument>${project.version}</argument>
                <argument>${git.commit.id}</argument>
                <argument>${build.time}</argument>
                <argument>${project.basedir}/target/generated-sources/java</argument>
              </arguments>
            </configuration>
          </execution>
        </executions>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-dependency-plugin</artifactId>
        <executions>
          <execution>
            <id>copy-dependencies</id>
            <phase>package</phase>
            <goals>
              <goal>copy-dependencies</goal>
            </goals>
            <configuration>
              <outputDirectory>${project.build.directory}/lib</outputDirectory>
              <overWriteReleases>false</overWriteReleases>
              <overWriteSnapshots>true</overWriteSnapshots>
              <excludeTransitive>false</excludeTransitive>
            </configuration>
          </execution>
        </executions>
      </plugin>

      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-surefire-plugin</artifactId>
        <configuration>
          <includes>
            <include>**/*Test.java</include>
          </includes>
          <forkCount>${surefire-forkcount}</forkCount>
          <reuseForks>false</reuseForks>
          <argLine>-Xmx512m -Dtest.junit.threads=${surefire-forkcount} -Dzookeeper.junit.threadid=${surefire.forkNumber} -javaagent:${org.jmockit:jmockit:jar}</argLine>
          <basedir>${project.basedir}</basedir>
          <redirectTestOutputToFile>true</redirectTestOutputToFile>
          <systemPropertyVariables>
            <build.test.dir>${project.build.directory}/surefire</build.test.dir>
            <zookeeper.DigestAuthenticationProvider.superDigest>super:D/InIHSb7yEEbrWz8b9l71RjZJU=</zookeeper.DigestAuthenticationProvider.superDigest>
          </systemPropertyVariables>
        </configuration>
      </plugin>

      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-jar-plugin</artifactId>
        <executions>
          <execution>
            <id>publish-test-jar</id>
            <goals>
              <goal>test-jar</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
     </plugins>
  </build>

</project>

```

2、把conf目录的log4j复制到resources目录发现没有日志输出

不知道为啥，下载下来的源码resources目标没有被Mark resources root，需要手动标记一下