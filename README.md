Maven Parents
=============

root-parent
-----------

This is the root parent with basic plugins and profiles. It automatically checks classpath for duplicate classes with
[duplicate-finder], checks Java code with [checkstyle] \(rules are defined in [checkstyle.xml]), runs integration tests,
collects metrics for code coverage analysis (when **ci** profile enabled), deploys sources and JavaDocs in deploy phase
etc.

It’s preconfigured to deploy released artifacts to [Bintray] (a [gateway][[bintray-maven-central] to the Maven Central) and snapshots to [oss.jfrog.org](https://oss.jfrog.org) (read [here][jfrog-oss]).

### Properties

*  **java.version** ... Version of JDK to compile sources for (default is 1.7).
*  **slf4j.version** ... Version of [slf4j-api] to use (default is 1.7.12).
*  **bintray.repo** ... A target repository in Bintray for releases, in the format of `{username}/{repository}` (default is jirutka/maven).
*  **bintray.package** ... A target package name under the Bintray repository (default is `${project.artifactId}`).

### Profiles

*  **ci** ... General profile for [CI] to analyze code coverage (uses [JaCoCo]). It should be activated automatically
   on CI environments (incl. Travis].
*  **travis-ci** ... Profile for [Travis] to submit code coverage to [Coveralls]. It’s activated automatically on Travis.

### Usage

Add this to the top of your POM:

```xml
<parent>
    <groupId>cz.jirutka.maven</groupId>
    <artifactId>root-parent</artifactId>
    <version>1.1.10</version>
</parent>
```

If you want to use Travis with Coveralls, put `.travis.yml` to the root of your repository:

```yml
language: java
sudo: false
jdk:
  - openjdk7
  - oraclejdk8
script:
  - 'mvn verify -B'
after_success:
  - 'mvn jacoco:report coveralls:jacoco'
```

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/cz.jirutka.maven/root-parent/badge.svg)](https://maven-badges.herokuapp.com/maven-central/cz.jirutka.maven/root-parent)


groovy-parent
-------------
_inherits from root-parent_

Parent for projects that uses Groovy.

### Properties

*  **groovy.version** ... Version of [groovy] to use.
*  **groovy-compiler.version** ... Version of [groovy-eclipse-compiler] to use.
*  **groovy-batch.version** ... Version of [groovy-eclipse-batch] to use.

### Usage

Add this to the top of your POM:

```xml
<parent>
    <groupId>cz.jirutka.maven</groupId>
    <artifactId>groovy-parent</artifactId>
    <version>1.1.10</version>
</parent>
```

If you want to use Groovy just in tests, not a production code, then redefine the groovy’s dependency scope:

```xml
<dependencies>
    <dependency>
        <groupId>org.codehaus.groovy</groupId>
        <artifactId>groovy</artifactId>
        <scope>test</scope>
    </dependency>
</dependencies>
```

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/cz.jirutka.maven/groovy-parent/badge.svg)](https://maven-badges.herokuapp.com/maven-central/cz.jirutka.maven/groovy-parent)


groovy-lombok-parent
--------------------
_inherits from groovy-parent_

Parent for projects that uses Groovy (mainly for tests) and [Lombok] annotation processor.

### Properties

*  **lombok.version** ... Version of [lombok] to use.

### Usage

Add this to the top of your POM:

```xml
<parent>
    <groupId>cz.jirutka.maven</groupId>
    <artifactId>groovy-lombok-parent</artifactId>
    <version>1.1.10</version>
</parent>
```

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/cz.jirutka.maven/groovy-lombok-parent/badge.svg)](https://maven-badges.herokuapp.com/maven-central/cz.jirutka.maven/groovy-lombok-parent)


License
-------

This project is licensed under [MIT license](http://opensource.org/licenses/MIT).


<!-- Links -->

[checkstyle]: http://checkstyle.sourceforge.net/
[CI]: http://en.wikipedia.org/wiki/Continuous_integration
[Coveralls]: https://coveralls.io/
[JaCoCo]: http://www.eclemma.org/jacoco/
[Maven Central]: http://search.maven.org/
[Lombok]: http://projectlombok.org/
[Bintray]: https://bintray.com/
[Travis]: https://travis-ci.org/
[bintray-maven-central]: http://blog.bintray.com/2014/02/11/bintray-as-pain-free-gateway-to-maven-central
[jfrog-oss]: http://www.jfrog.com/confluence/pages/viewpage.action?pageId=26083425

[checkstyle.xml]: /codequality-resources/src/main/resources/cz/jirutka/maven/codequality/checkstyle.xml

[groovy]: http://search.maven.org/#search|gav|1|g%3A%22org.codehaus.groovy%22%20AND%20a%3A%22groovy%22
[groovy-eclipse-batch]: http://search.maven.org/#search|gav|1|g%3A%22org.codehaus.groovy%22%20AND%20a%3A%22groovy-eclipse-batch%22
[groovy-eclipse-compiler]: http://search.maven.org/#search|gav|1|g%3A%22org.codehaus.groovy%22%20AND%20a%3A%22groovy-eclipse-compiler%22
[lombok]: http://search.maven.org/#search|gav|1|g%3A%22org.projectlombok%22%20AND%20a%3A%22lombok%22
[slf4j-api]: http://search.maven.org/#search|gav|1|g%3A%22org.slf4j%22%20AND%20a%3A%22slf4j-api%22
