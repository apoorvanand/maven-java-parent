Maven Parent for Java Projects
-----
This project holds the core bill of materials for Java projects at Microsoft. Libraries and SDKs can reference these parent POMs to ensure they are up to date with the latest Maven
plugins and configurations for Maven builds.

Projects that must be compliant with Java 8 may use the `java-8-parent` POM. Projects that can be compliant with Java 11 may use the `java-11-parent` POM.

## Instructions

To configure your Maven project to use these POMs, copy the respective configuration into your core `pom.xml` file (e.g. for multi-module Maven projects, paste this into your main
`pom.xml`).

### Java 8

```xml
    <parent>
        <groupId>com.microsoft</groupId>
        <artifactId>maven-java-8-parent</artifactId>
        <version>8.0.0-SNAPSHOT</version>
    </parent>
```

### Java 11

```xml
    <parent>
        <groupId>com.microsoft</groupId>
        <artifactId>maven-java-11-parent</artifactId>
        <version>11.0.0-SNAPSHOT</version>
    </parent>
```

# Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.microsoft.com.

When you submit a pull request, a CLA-bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., label, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
