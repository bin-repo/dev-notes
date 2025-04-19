# sonatype-nexus-repo（私有仓库使用方法）

## Maven环境配置（settings.xml）

### 设置`本地仓库`（默认为${user.home}/.m2/repository）

```xml
<localRepository>指定本地仓库位置</localRepository>
```

### 设置`仓库服务`（应用发布到nexus私有仓库时需验证用户及口令）

```xml
<servers>
    <server>
        <id>nexus-releases</id>
        <username>用户</username>
        <password>口令</password>
    </server>
    <server>
        <id>nexus-snapshots</id>
        <username>用户</username>
        <password>口令</password>
    </server>
</servers>
```

### 设置`仓库地址`

```xml
<mirrors>
    <mirror>
        <id>nexus-releases</id>
        <mirrorOf>*</mirrorOf>
        <url>http://localhost:8081/repository/repo-public/</url>
    </mirror>
    <mirror>
        <id>nexus-snapshots</id>
        <mirrorOf>*</mirrorOf>
        <url>http://localhost:8081/repository/repo-public/</url>
    </mirror>
</mirrors>
```

### 设置`环境参数`

```xml
<profiles>
    <profile>
        <id>nexus</id>
        <repositories>
            <repository>
                <id>nexus-releases</id>
                <url>http://nexus-releases</url>
                <releases><enabled>true</enabled></releases>
                <snapshots><enabled>true</enabled></snapshots>
            </repository>
            <repository>
                <id>nexus-snapshots</id>
                <url>http://nexus-snapshots</url>
                <releases><enabled>true</enabled></releases>
                <snapshots><enabled>true</enabled></snapshots>
            </repository>
        </repositories>
        <pluginRepositories>
            <pluginRepository>
                <id>nexus-releases</id>
                <url>http://nexus-releases</url>
                <releases><enabled>true</enabled></releases>
                <snapshots><enabled>true</enabled></snapshots>
            </pluginRepository>
            <pluginRepository>
                <id>nexus-snapshots</id>
                <url>http://nexus-snapshots</url>
                <releases><enabled>true</enabled></releases>
                <snapshots><enabled>true</enabled></snapshots>
            </pluginRepository>
        </pluginRepositories>
    </profile>
</profiles>
<!-- 生效的环境参数 -->
<activeProfiles>
    <activeProfile>nexus</activeProfile>
</activeProfiles>
```

## Maven项目配置（pom.xml）

- 仓库ID必须与setting.xml中的server的ID保持一致

```xml
<distributionManagement>
    <repository>
        <id>nexus-releases</id>
        <name>Nexus Release Repository</name>
        <url>http://localhost:8081/repository/repo-release/</url>
    </repository>
    <snapshotRepository>
        <id>nexus-snapshots</id>
        <name>Nexus Snapshot Repository</name>
        <url>http://localhost:8081/repository/repo-snapshot/</url>
    </snapshotRepository>
</distributionManagement>
```

## 发布Jar包（安装到本地仓库并发布到私有仓库）

```sh
mvn deploy
```

## Gradle项目配置（样例）

```text
allprojects {
    repositories {
        maven {
            url "http://localhost:8081/repository/repo-public/"
        }
    }
    buildscript {
        ext {
            springBootVersion = '1.5.4.RELEASE'
        }
        repositories {
            maven {
                url "http://localhost:8081/repository/repo-public/"
            }
        }
    }
}

apply plugin: 'java'
apply plugin: 'maven'

group = 'com.example'
version = '0.0.1-SNAPSHOT'
sourceCompatibility = 1.8

dependencies {
    compile("org.springframework.boot:spring-boot-starter-web:${springBootVersion}")
    testCompile("org.springframework.boot:spring-boot-starter-test:${springBootVersion}")
}

uploadArchives {
    configuration = configurations.archives
    repositories {
        mavenDeployer {
            repository(url: "http://localhost:8081/repository/repo-release/") {
                authentication(userName: "admin", password: "admin123")
            }
            pom.project {
                name 'demo'
                version '0.0.1'
                artifactId 'demoTest'
                groupId 'com.example'
                packaging 'aar'
                description 'demo for test'
            }
        }
    }
}
```

```sh
upload
uploadArchives
```
