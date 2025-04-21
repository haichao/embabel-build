![Apache Maven](https://img.shields.io/badge/Apache%20Maven-C71A36?style=for-the-badge&logo=Apache%20Maven&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white)

<img align="left" src="https://github.com/embabel/agent-api/blob/main/images/315px-Meister_der_Weltenchronik_001.jpg?raw=true" width="180">

&nbsp;&nbsp;&nbsp;&nbsp;


# Embabel Build

## Overview
Embabel Build is a comprehensive multi-module Maven project that provides a standardized build infrastructure for all Embabel projects. This parent POM centrally manages plugins and dependencies, ensuring consistency, quality, and compliance across the enleadtire Embabel ecosystem while reducing redundant configuration and technical debt.

## Project Structure
The project is organized into the following modules:

- **embabel-build-parent**: The root parent POM providing global configuration
- **embabel-build-dependencies**: Central BOM (Bill of Materials) for dependency versioning
- **embabel-dependencies-parent**: Parent module for consistent configuration inheritance

## Design Goals

### Standardized Build Management
The Embabel Build system provides a robust and consistent build infrastructure across all Embabel projects through a parent POM that manages plugins and dependencies centrally:

- **Single Source of Truth**: Eliminates redundant configuration and ensures version consistency
- **Plugin Management**: Pre-configures build plugins with best practices
- **Profile Management**: Defines common profiles like `skip-tests` for development efficiency
- **Repository Configuration**: Centralizes repository definitions for Spring milestones and snapshots
- **Distribution Management**: Configures GitHub package repository for artifact distribution

### Kotlin-First Development
The build system is optimized for Kotlin development (version 2.1.10) with specific compiler settings and Spring integration, while maintaining Java 21 compatibility:

- **Advanced Kotlin Configuration**:
  - Strict JSR-305 null safety with `-Xjsr305=strict`
  - API version set to Kotlin 2.1
  - Automatic Spring integration via the Kotlin Spring compiler plugin
  - Java parameters reflection support (javaParameters=true)
  - Source directory configuration for generated code handling

- **Kotlin-Java Interoperability**: 
  - Careful configuration of Maven compiler plugin executions
  - Coordinated compile phases between Java and Kotlin sources

### Spring Framework Integration
The build system seamlessly integrates with Spring Framework:

- **Spring Boot Compatibility**: Configured for Spring Boot 3.4.3
- **Spring Plugin Integration**: Kotlin compiler configured with Spring plugin for automatic component detection
- **Annotation Processing**: Configuration for handling Spring's annotation processing
- **Resource Handling**: Customized resource filtering and processing for Spring applications

### Modular Architecture
The build system supports multi-module structure:

- **Shared Kernel**: The parent POM acts as a shared kernel for build functionality
- **Module Composition**: Facilitates composition of modules into higher-level aggregates
- **Dependency Isolation**: Helps maintain proper module boundaries and dependencies

### Quality Assurance

- **Code Coverage**: 
  - JaCoCo for detailed code coverage reporting
  - XML and HTML report generation
  - Integration with SonarCloud

- **Code Style**: 
  - Spotless for Kotlin code style enforcement
  - Custom formatting rules
  - Automatic formatting during build

- **Testing**: 
  - Surefire for test management 
  - Flaky test detection (failOnFlakeCount=1)
  - Automatic rerun of failing tests (rerunFailingTestsCount=1)
  - Exclusion of integration tests from unit test phase

- **Static Analysis**: 
  - SonarCloud integration
  - Language-specific analyzer configuration
  - Quality gate enforcement

### Dependency Management
Centralizes dependency version control through a sophisticated BOM approach:

- **Version Coordination**: Makes version management consistent across all modules
- **Conflict Resolution**: Reduces dependency conflicts through enforcer plugin
- **Transitive Dependency Management**: Controls the propagation of dependencies
- **Scope Management**: Defines appropriate scopes for dependencies
- **Exclusion Management**: Handles problematic transitive dependencies

### License Compliance
Automates license tracking and documentation generation to ensure proper legal compliance:

- **License Reports**: 
  - Generates third-party license reports
  - Creates aggregate license lists
  - Manages license files for distribution

- **Dependency Documentation**:
  - Creates detailed dependency trees
  - Documents transitive dependencies
  - Sorts dependencies by group and artifact for readability

- **License Validation**:
  - Ensures all dependencies have compatible licenses
  - Documents license exceptions where needed

### CI/CD Integration
Embabel Build supports robust integration with CI/CD pipelines:

- **SonarCloud**: 
  - Configured for code quality metrics
  - Organization-specific settings
  - Coverage report integration

- **GitHub Integration**:
  - Package repository distribution
  - SCM connection configuration
  - Developer information

- **Git Metadata**:
  - Captures git commit IDs
  - Tracks branch information
  - Records commit timestamps
  - Embeds git properties in built artifacts

### Reproducible Builds
Ensures reliable, reproducible builds through explicit configuration:

- **Encoding Configuration**: 
  - UTF-8 for source encoding
  - UTF-8 for output encoding
  - UTF-8 for reporting

- **Compiler Settings**:
  - Java 21 source and target compatibility
  - Explicit JVM target for Kotlin
  - Standardized compiler arguments

- **POM Flattening**:
  - OSS-compliant POM generation
  - Removal of build-specific elements
  - Consistent POM structure for distribution

### Documentation and Metadata
Automates the generation of comprehensive documentation:

- **Dependency Documentation**:
  - Dependency trees
  - Third-party license lists
  - Version information

- **Build Metadata**:
  - Git commit information
  - Build timestamps
  - Version details

- **Distribution Information**:
  - Organization metadata
  - Developer contact information
  - SCM repository links

## Usage

### Using Embabel Build as Parent

To use Embabel Build as a parent for your project:

```xml
<parent>
    <groupId>com.embabel.build</groupId>
    <artifactId>embabel-build-parent</artifactId>
    <version>1.0.0-SNAPSHOT</version>
</parent>
```

### Importing Dependency Management

To use only the dependency management without inheriting other configurations:

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>com.embabel.build</groupId>
            <artifactId>embabel-build-dependencies</artifactId>
            <version>1.0.0-SNAPSHOT</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

### Available Profiles

- **skip-tests**: Skips all tests during build (`mvn clean install -Pskip-tests`)

## Plugin Configuration

Embabel Build preconfigures numerous plugins to ensure consistent builds. Key plugins include:

- **kotlin-maven-plugin**: Configured for Spring integration and strict null safety
- **maven-compiler-plugin**: Set up for Java 21 compatibility
- **jacoco-maven-plugin**: Configured for code coverage reporting
- **spotless-maven-plugin**: Set up for Kotlin code style enforcement
- **git-commit-id-plugin**: Configured to capture Git metadata
- **license-maven-plugin**: Set up for license compliance reporting
- **maven-dependency-plugin**: Configured for dependency analysis
- **flatten-maven-plugin**: Set up for POM flattening and OSS compliance

## Requirements

- Java 21 or higher
- Maven 3.8+ 
- Git (for git-commit-id-plugin functionality)

## License

Apache License, Version 2.0

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for details on how to contribute to this project.

## Team

The project is maintained by the Embabel development team:

- Rod Johnson (Founder and Project Lead)
- Alex Hein-Heifetz (Lead)
- Igor Dayen (Lead)

## Links

- [Project Website](https://embabel.com/embabel)
- [GitHub Repository](https://github.com/embabel/embabel-build)
- [Issue Tracker](https://github.com/embabel/embabel-build/issues)
