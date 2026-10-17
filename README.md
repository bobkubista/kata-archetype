# kata-archetype

This is a maven archetype for creating code kata projects.

Usage: the archetype is not on Maven Central, so install it locally first (`mvn install` in this repo), then generate a kata:

```
mvn archetype:generate -DarchetypeGroupId=com.bobkubista -DarchetypeArtifactId=kata-archetype -DarchetypeVersion=0.0.1-SNAPSHOT
```

A generated kata gets a `pom.xml` (Java 25, JUnit, JaCoCo, Spotless with `formatter.xml`, SonarQube scanner), a `Jenkinsfile` for the kvm-server Jenkins and a `.gitignore`.

## Build

Requires Java 25 and Maven 3.9 or newer. `mvn verify` builds the archetype and runs its integration test: it generates a kata from `src/test/resources/projects/basic` and runs `mvn verify` on it.
