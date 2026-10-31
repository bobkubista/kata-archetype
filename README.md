# kata-archetype

This is a maven archetype for creating code kata projects.

Usage: the archetype is not on Maven Central, so install it locally first (`mvn install` in this repo), then generate a kata:

```
mvn archetype:generate -DarchetypeGroupId=com.bobkubista -DarchetypeArtifactId=kata-archetype -DarchetypeVersion=0.0.1-SNAPSHOT
```

A generated kata gets a `pom.xml` (Java 25, JUnit, JaCoCo, Spotless with `formatter.xml`, SonarQube scanner), a `Jenkinsfile` for the kvm-server Jenkins and a `.gitignore`.

## Build

Requires Java 25 and Maven 3.9 or newer. `mvn verify` builds the archetype and runs its integration test: it generates a kata from `src/test/resources/projects/basic` and runs `mvn verify` on it.

## Dependency updates

Renovate (`renovate.json`, the shared `bobkubista/renovate-config` preset) also updates the template
pom in `src/main/resources/archetype-resources/pom.xml` on purpose: new katas start on current
versions. The integration test above proves that the updated template still generates and builds, so
merge a Renovate PR only when its Jenkins build is green.
