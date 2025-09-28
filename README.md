# Java Parent POM

A shared **Maven parent project** that provides a consistent baseline for all Java modules.

## Features

**Common dependencies**
- Lombok
- Apache Commons Lang3
- Apache Commons Collections4
- SLF4J API (with `slf4j-simple` for tests)
- JUnit Jupiter

**Build quality plugins (bound in order)**

1. **Spotless + Palantir Java Format** — automatic code formatting
2. **Checkstyle** — style/lint rules
3. **SpotBugs** — static analysis
4. **Surefire** — unit tests
5. **Failsafe** — integration tests
6. **JaCoCo** — code coverage check

**Enforcer plugin ensures**
- Minimum Java and Maven versions
- Dependency convergence
- No snapshot dependencies

## Usage

1. Inherit from this parent the new project's `pom.xml`:

```xml
<parent>
  <groupId>com.example</groupId>
  <artifactId>java-parent</artifactId>
  <version>1.0.0</version>
</parent>
```

2. Copy the `LICENSE` file to the new project's base directory directory:

The contents of this file is automatically applied to all Java files by the Spotless plugin and configured via the `licenseHeader` option.

```bash
$ java-project/LICENSE
```

3. Copy `checkstyle-suppressions.xml` to the new project's base directory:

These suppressions are necessary to ensure compatibility with `palantir-java-format` which cannot be modified.

```bash
$ java-project/checkstyle-suppressions.xml
```

## Build Lifecycle

validate → format (Spotless) → compile → checkstyle → spotbugs → test (Surefire) → integration-test (Failsafe) → verify (coverage, reports)


