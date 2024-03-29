|   Author        |  Created on   |  Version   | Last updated by  | Last edited on |
| --------------- | --------------| -----------|----------------- | -------------- |
| Khushi Malhotra |  30 Jan 2024  |  Version 1 | Khushi Malhotra  | 31 Jan 2024    |
***

# Code Compilation - Go language CI Checks 

# Table of Contents
- [What is Code Compilation in CI Checks](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Design/05-%20GoLang%20CI%20Checks/Code_Compilation_GoLang.md#what-is-code-compilation-in-ci-checks)
- [Why we need Code Compilation](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Design/05-%20GoLang%20CI%20Checks/Code_Compilation_GoLang.md#why-we-need-code-compilaton)
- [Different tools used in Code Compilation of Go lang](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Design/05-%20GoLang%20CI%20Checks/Code_Compilation_GoLang.md#different-tools-used-in-code-compilation-of-go-lang)
- [Comparison between go build and go tool compile](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Design/05-%20GoLang%20CI%20Checks/Code_Compilation_GoLang.md#comparison-between-go-build-and-go-tool-compile)
- [Is go build better than go tool compile?](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Design/05-%20GoLang%20CI%20Checks/Code_Compilation_GoLang.md#is-go-build-better-than-go-tool-compile)
- [Conclusion](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Design/05-%20GoLang%20CI%20Checks/Code_Compilation_GoLang.md#conclusion)
- [Contact Information](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Design/05-%20GoLang%20CI%20Checks/Code_Compilation_GoLang.md#contact-information)
- [Resources and References](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Design/05-%20GoLang%20CI%20Checks/Code_Compilation_GoLang.md#resources-and-references)
***
# What is Code Compilation in CI Checks
Code compilation in CI checks refers to the process of compiling the source code of a project as part of a Continuous Integration (CI) pipeline. 
CI is a software development practice that involves automatically building and testing code changes made by developers, ensuring that the code is free of errors and adheres to the rules of the programming language.

# Why we need Code Compilaton
| Feature                     | Description                                                                                                                                                                 |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Early Error Detection**   | Compilation catches syntax errors, type mismatches, and other code-level issues early in the development process. Identifying these problems before testing and deployment prevents costly downstream issues and saves time. |
| **Dependency Management**   | Go's dependency management system (go mod) relies on compilation to ensure proper version resolution and compatibility of packages. CI compilation verifies that dependencies are correctly fetched and integrated, reducing dependency-related errors. |
| **Static Analysis**         | Go's compiler supports built-in static analysis tools like go vet and golint. Integrating these tools into the CI compilation stage checks for potential code problems, code style violations, and security vulnerabilities, enhancing code quality. |
| **Cross-Platform Compatibility** | Go produces platform-specific binaries. Compiling in CI for different target platforms (e.g., Windows, Linux, macOS) ensures code compatibility across environments, preventing deployment issues. |
| **Reproducible Builds**     | Go's deterministic compilation process ensures consistent binaries for the same code and dependencies. This reproducibility is crucial for reliable testing, deployment, and auditing in CI environments. |
| **Fast Feedback Cycle**     | Go's compilation is relatively fast, providing quick feedback on code changes. This enables developers to quickly identify and fix errors, contributing to a smoother development process. |
| **Versioning**              | Go's compilation can be used for version control, tracking changes and managing different software versions effectively.                                                    |

# Different tools used in Code Compilation of Go Lang
| **Compilation Tool for Go** | **Description**                                                                                                   |
|-----------------------------|-------------------------------------------------------------------------------------------------------------------|
| **go build**             | - Compiles entire Go projects, including dependencies.<br>- Generates an executable binary for immediate use.    |
| **go tool compile**      | - Compiles individual Go packages into object files (.o).<br>- Lower-level tool suitable for specific tasks like debugging or custom build processes. |

# Comparison between go build and go tool compile
| **Aspect**                    | **go build**                                                                                               | **go tool compile**                                                                                                       |
|-------------------------------|------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| **Description**               | - Compiles entire project with dependencies.<br>- Generates an executable binary.                          | - Compiles individual Go packages into object files (.o).<br>- A lower-level tool for specific tasks like debugging.       |
| **Output**                    | - Produces an executable binary (.exe, .out) ready to run your program.                                    | - Generates individual object files (.o) containing compiled code for a specific package.<br>- Further linking is needed to create an executable.                                  |
| **Use Cases**                 | - Building executables for testing, deployment, and running applications.<br>- Everyday development needs.  | - Debugging specific code sections by inspecting generated assembly.<br>- Integrating compilation into custom build systems or workflows.<br>- Understanding the internal workings of the Go compiler.  |
| **Advantages**                | - Convenience: Handles everything in one step, including dependency resolution and linking.<br>- Simplicity: Easy to use and understand, ideal for everyday development tasks.<br>- Automation: Integrates seamlessly with build tools and CI pipelines.<br>- Output: Produces directly runnable executables for immediate testing and deployment. | - Granularity: Offers fine-grained control over individual package compilation.<br>- Debugging: Enables inspection of assembly code for specific packages.<br>- Customization: Useful for building complex programs with custom workflows.<br>- Learning: Provides insights into the internal workings of the Go compiler. |


# Is go build better than go tool compile?
It depends on your needs!go build is generally better for most developers due to its simplicity and convenience for building complete applications.
However, go tool compile has its own advantages for specific situations where fine-grained control or deep understanding of the compilation process is crucial.
Here simplicity and building a complete application are key, I'll stick with the convenience of go build.

# Commands used with go build
| Command        | Purpose                                                      | How it Works                                                                                                                                                                           | What it Checks                                                                                              | When to Use                                                              |
|----------------|--------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| `go mod tidy`  | Maintains the go.mod file, reflecting actual dependencies.  | Identifies and removes unused dependencies. Adds new dependencies and updates their versions. May update the minimum Go version compatible with dependencies.                     | Unused dependencies, updates versions, may update minimum Go version compatibility.                         | Regularly, after adding or removing dependencies. Before sharing or committing changes.                                               |
| `go vet`       | Identifies potential issues and weaknesses in Go code.       | Static analysis for:   - Unused variables, functions, and imports.    Inefficient code patterns.    Suspicious code constructs.   - Possible errors.                                  | Unused variables, inefficient code patterns, suspicious constructs, possible errors.                        | During development to find and fix problems early. As part of CI/CD pipeline.                                                          |
| `go lint`      | Enforces code style and formatting consistency.              |  Uses configurable rules to check code against style guidelines. Offers suggestions but doesn't automatically fix issues.                                                            | Code style and formatting consistency.                                                                     | To maintain code readability and consistency. As part of CI/CD pipeline to enforce style rules.                                      |
| `go build`     | Compiles Go source code into an executable binary.            |  Reads go.mod for dependencies. - Downloads and builds required dependencies.  Compiles source code into object files. - Links object files into the final executable.           | Compilation, linking, dependency management.                                                               | When you need to run your Go program. As part of CI/CD pipeline for deployment.                                                       |
| `go test`      | Executes unit tests defined in Go code.                       |  Discovers and runs test functions using specific naming conventions.  Reports test failures.                                                                                        | Unit test execution, test failure reporting.                                                               | Regularly during development to ensure code works as expected. As part of CI/CD pipeline to verify correctness before deployment.    |


> [!NOTE]
> POC for go code compilation is prepared in different doc,if you want to see the code compilation of go use this link [go POC](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Design/05-%20GoLang%20CI%20Checks/Code_compilationPOC-go.md) 

***

# Conclusion
- Go's straightforward compilation process, combined with built-in tools for dependency management, static analysis, and testing, promotes code quality and reliability.
- Following these steps ensures a smooth development workflow and confidence in code functionality.
- By integrating these tools into build systems or CI pipelines, you can automate quality checks and catch issues early, leading to more robust and maintainable Go applications.

# Contact Information
| Name            | Email Address                        |
|-----------------|--------------------------------------|
| Khushi Malhotra | khushi.malhotra.snaatak@mygurukulam.co |

# Resources and References
[Code Compilation](https://www.techtarget.com/searchsoftwarequality/CI-CD-pipelines-explained-Everything-you-need-to-know) 

[POC](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Design/05-%20GoLang%20CI%20Checks/Code_compilationPOC-go.md) 
