Changelog
====

### 3.8

Release date: 2018 Apr 10

* Update Jenkins Test Harness from 2.34 to 2.38
([Changelog](https://github.com/jenkinsci/jenkins-test-harness/#changelog))

### 3.7

Release date: 2018 Apr 03

* Access modifier checker plugin updated to 1.14 and synchronized with the annotation library; introduces `@Restricted(Beta.class)` which may be consumed in a downstream plugin by setting the POM property `useBeta` to `true`.

### 3.6

Release date: 2018 Mar 09

* Access modifier checker plugin updated, making checks more strict in some cases, such as `@Restricted(NoExternalUse.class)` on a type. You may pass `-Daccess-modifier-checker.failOnError=false` as a temporary workaround.
* Animal Sniffer plugin updated, fixing errors in certain cases, such as use of Java 9-enabled libraries.

### 3.5

Release date: 2018 Feb 19

* [PR #95](https://github.com/jenkinsci/plugin-pom/pull/95) - extend bytecode rule fix made in 3.2 to `task-reactor`, needed for testing against Jenkins 2.105 and later.

### 3.4

* [PR #94](https://github.com/jenkinsci/plugin-pom/pull/94) - update `jenkins-test-harness` and `maven-hpi-plugin`.

### 3.3

* [PR #84](https://github.com/jenkinsci/plugin-pom/pull/84) -
Make FindBugs effort and threshold options configurable.

### 3.2

* Ignore Java 8 bytecode coming from Remoting and Stapler, permitting plugins with `java.level=7` to still build (for example from `Jenkinsfile`) with, for example, `jenkins.version=2.89`.
* Run tests in alphabetical order.

### 3.1

* Force `java.level` to be specified in each POM. 3.0 had changed the default value to `8`, causing plugins which had only overridden `jenkins.version` (to something older to 2.60.x) to not be runnable on older Jenkins installations using Java 7.
* Fail early if using JDK 7 or earlier to build. (`java.level=7` is fine.)
* `jenkins-test-harness` updated to [2.32](https://github.com/jenkinsci/jenkins-test-harness/#232-2017-oct-28).

### 3.0

* [PR#83](https://github.com/jenkinsci/plugin-pom/pull/83) **DROP SUPPORT FOR JENKINS 1.x**
* [PR#87](https://github.com/jenkinsci/plugin-pom/pull/87) Configure the _maven-javadoc-plugin_ to link back to the Jenkins Javadoc

### 2.37

Release date: 2017, Oct 23

* `jenkins-test-harness` updates to [2.31](https://github.com/jenkinsci/jenkins-test-harness/#231-2017-oct-17), important for testing against core 2.86+
* `concurrency` property deprecated; use `forkCount` instead
* FindBugs Maven plugin update to 3.0.5

### 2.36

Release date: 2017, Sep 27

* `jenkins-test-harness` updated to [2.28](https://github.com/jenkinsci/jenkins-test-harness/#228-2017-sep-26)
* `maven-hpi-plugin` updated to [2.1](https://github.com/jenkinsci/maven-hpi-plugin#21-2017-sep-26)

### 2.35

Release date: 2017, Sep 20

* JENKINS-45245: allow IntelliJ IDEA to run `JenkinsRule`-based tests, broken since 2.30 due to a mismatch with Maven’s idea of the test classpath.

### 2.34

Release date: 2017, Sep 18

* [PR #74](https://github.com/jenkinsci/plugin-pom/pull/74) -
Annotate `Messages` classes generated by Localizer with `@Restricted(NoExternalUse.class)`
  * If the message is exposed intentionally, it is recommended to expose it via Java API class instead of a generated one.
* [PR #71](https://github.com/jenkinsci/plugin-pom/pull/71) - 
Specify the default Max Memory for Maven Surefire Plugin (768MB).

### 2.33

Release date: 2017, Aug 07

* JENKINS-41631 amendment to work better on new cores.

### 2.32

Release date: 2017, Jun 29

* JENKINS-41631 amendment to support 1.585- core versions.

### 2.31

Release date: 2017, Jun 26

* JENKINS-41631: use `requireUpperBoundDeps` to prevent various common versioning problems, such as accidentally using incompatible plugin dependencies.
* JENKINS-44453: JenkinsRule should ensure that Jenkins reaches the COMPLETED milestone.

### 2.30

Release date: 2017, May 25

* Integrated `maven-hpi-plugin` 2.0:
  * The `war-for-test` artifact is no longer needed for functional tests, saving download bandwidth.
  * Bundled Jetty was updated, so JDK 8 is required at build time.
* Setup Wizard disabled by default when using `hpi:run`. To enable it use `-Dhudson.Main.development=false`.

### 2.29

Release date: 2017, May 19

* For plugins which use npm, load node and npm binaries from the Jenkins Artifactory rather than a third-party server; yarn-based plugins load just the node binary from Artifactory.

### 2.28

Release date: 2017, May 04

* Updated `access-modifier-checker` to fix a critical bug (lack of enforcement of any method calls).

### 2.27

Release date: 2017, May 02

* Updated `maven-hpi-plugin`, `jenkins-test-harness`, and more.
* Support for building JavaScript libraries with yarn.
* Ability to specify `jenkins-core.version` and `jenkins-war.version` separately so as to depend on timestamped snapshots of Jenkins core.

### 2.26

* Update `frontend-maven-plugin` from `1.3` to `1.4` ([PR#53](https://github.com/jenkinsci/plugin-pom/pull/53))
* Update all maven plugins to latest ([PR#54](https://github.com/jenkinsci/plugin-pom/pull/54))

### 2.25

Release date: 2017, Mar 22

* [JENKINS-42800](https://issues.jenkins-ci.org/browse/JENKINS-42800) - 
Bump JaCoCo version from `0.7.2.201409121644` to `0.7.9` to be compatible with [Jenkins JaCoCo plugin](https://plugins.jenkins.io/jacoco) data format.

Compatibility notes:
* The change introduces the new reporting format in JaCoCo. 
It may cause regressions in build flows which have the `enable-jacoco` profile enabled.

### 2.24

Release date: 2017, Mar 08

* Updated `frontend-maven-plugin` and `download-maven-plugin` for the benefit of plugins using npm.
* Removed broken attempt to activate `enable-jacoco` profile by default. Now disabled unless selected.

### 2.23

Release date: 2017, Feb 22

* Using [version 2.18](https://github.com/jenkinsci/jenkins-test-harness#218-2016-dec-20) of the test harness.

### 2.22

Release date: 2017, Feb 13

* Updated `maven-hpi-plugin` for better snapshot behavior.

### 2.21

Release date: 2017, Jan 19

* Default to `concurrency=1`. To run faster tests locally, use for example
```xml
<profile>
    <id>faster</id>
    <activation>
        <activeByDefault>true</activeByDefault>
    </activation>
    <properties>
        <concurrency>1C</concurrency>
    </properties>
</profile>
```

### 2.20

Release date: 2017, Jan 14

* Default to non-verbose javadoc generation logs.
([PR #41](https://github.com/jenkinsci/plugin-pom/pull/41))

### 2.19

Release date: 2016, Nov 10

* Fixed a critical regression in 2.18.

### 2.18

This release is **BROKEN**, use 2.19 instead.

Release date: 2016, Nov 08

* Introduced `no-test-jar` property. 

This **Incompatible** for plugins declaring a `jar:test-jar` execution; you must use the new property instead.

### 2.17 and earlier

Changes not recorded.
