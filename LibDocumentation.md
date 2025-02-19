## Dependencies
Exposed modules are available from Maven Central (JFrog Bintray and JCenter for older version) repositories.
To use them you have to add appropriate dependency into your repositories mapping.

#### Maven
```xml
<!-- Versions after 0.30.1 -->
<repositories>
    <repository>
        <id>mavenCentral</id>
        <name>mavenCentral</name>
        <url>https://repo1.maven.org/maven2/</url>
    </repository>
</repositories>

<!-- Versions before 0.30.1 -->
<repositories>
    <repository>
        <id>jcenter</id>
        <name>jcenter</name>
        <url>https://jcenter.bintray.com</url>
    </repository>
</repositories>
```

#### Gradle Groovy and Kotlin DSL

```kotlin
repositories {
    // Versions after 0.30.1
    mavenCentral()

    // Versions before 0.30.1
    jcenter()
}
```

## Base Modules
### Exposed 0.17.x and lower
Prior Exposed 0.18.1 there was only one base module `exposed` which contains everything you may need including JodaTime as date-time library.
To add `Exposed` framework of that version you had to use: 
    
#### Maven
```xml
<dependencies>
  <dependency>
    <groupId>org.jetbrains.exposed</groupId>
    <artifactId>exposed</artifactId>
    <version>0.17.7</version>
  </dependency>
</dependencies>

```

#### Gradle Groovy
```groovy
dependencies {
  compile 'org.jetbrains.exposed:exposed:0.17.7'
}
```
#### Gradle Kotlin DSL
```kotlin
dependencies {
    compile("org.jetbrains.exposed", "exposed", "0.17.7")
}
```

### Exposed 0.18.1 and higher
To move forward and support such features as Java 8 Time, async drivers and so on it was decided to split Exposed into more specific modules. It will allow you to take the only modules you need and will add flexibility in the future.

At the moment `Exposed` coexists of five modules
* exposed-core - base module, which contains both DSL api along with mapping
* exposed-dao - DAO api 
* exposed-jdbc - transport level implementation based on Java JDBC API
* exposed-jodatime - date-time extensions based on JodaTime library
* exposed-java-time - date-time extensions based on Java8 Time API

Dependencies mapping listed bellow is similar (by functionality) to the previous versions:
#### Maven
```xml

<dependencies>
  <dependency>
    <groupId>org.jetbrains.exposed</groupId>
    <artifactId>exposed-core</artifactId>
    <version>0.31.1</version>
  </dependency>
  <dependency>
    <groupId>org.jetbrains.exposed</groupId>
    <artifactId>exposed-dao</artifactId>
    <version>0.31.1</version>
  </dependency>
  <dependency>
    <groupId>org.jetbrains.exposed</groupId>
    <artifactId>exposed-jdbc</artifactId>
    <version>0.31.1</version>
  </dependency>
  <dependency>
    <groupId>org.jetbrains.exposed</groupId>
    <artifactId>exposed-jodatime</artifactId>
    <version>0.31.1</version>
  </dependency>
  <dependency>
    <groupId>org.jetbrains.exposed</groupId>
    <artifactId>exposed-java-time</artifactId>
    <version>0.31.1</version>
  </dependency>
</dependencies>

```

#### Gradle Groovy
```groovy
dependencies {
  compile 'org.jetbrains.exposed:exposed-core:0.31.1'
  compile 'org.jetbrains.exposed:exposed-dao:0.31.1'
  compile 'org.jetbrains.exposed:exposed-jdbc:0.31.1'
  compile 'org.jetbrains.exposed:exposed-jodatime:0.31.1'
  // or
  compile 'org.jetbrains.exposed:exposed-java-time:0.31.1'
}
```
#### Gradle Kotlin DSL
In `build.gradle.kts`:
```kotlin
val exposedVersion: String by project
dependencies {
    implementation("org.jetbrains.exposed:exposed-core:$exposedVersion")
    implementation("org.jetbrains.exposed:exposed-dao:$exposedVersion")
    implementation("org.jetbrains.exposed:exposed-jdbc:$exposedVersion")
    implementation("org.jetbrains.exposed:exposed-jodatime:$exposedVersion")
    // or
    implementation("org.jetbrains.exposed:exposed-java-time:$exposedVersion")
}
```
and in `gradle.properties`
```
exposedVersion=0.31.1
```

### JDBC driver and logging
You also need a JDBC driver for the database system you are using (see [[DataBase and DataSource|DataBase-and-DataSource]]) and a logger for `addLogger(StdOutSqlLogger)`. Example (Gradle syntax):
```kotlin
dependencies {
    // for H2
    implementation("com.h2database:h2:1.4.199")
    // for logging (StdOutSqlLogger), see
    // http://www.slf4j.org/codes.html#StaticLoggerBinder
    implementation("org.slf4j:slf4j-nop:1.7.30")
}
```
