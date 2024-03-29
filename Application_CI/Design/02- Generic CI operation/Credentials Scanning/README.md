# Credential Scanning
![5_Best_Practices_for_Credentialed-Scanning_Header](https://github.com/avengers-p7/Documentation/assets/156056344/893d53ce-758a-418d-905c-07d30749e83c)

***
## Table Of Contents 
+ [Introduction](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Design/Credential%20Scanning.md#introduction)
+ [Why Credential Scanning](#why-credential-scanning-)
+ [Types Of Credentials](#types-of-credentials)
+ [When To Scan For Credentials](#when-to-scan-for-credentials)
+ [Credential Scanning Tools](#credential-scanning-tools)
+ [Tool Comparison](#tool-comparison)
+ [Tool Recommendation](#tool-recommendation)
+ [Proof Of Concept : GitLeaks](#proof-of-concept--gitleaks)
+ [Advantages](#advantages)
+ [Best Practices](#best-practices)  
+ [Conclusion](#conclusion)
+ [Contact Information](#contact-information)
+ [References](#references)

***
## Introduction 
Credential scanning is the practice of automatically inspecting a project to ensure that no secrets are included in the project's source code. Secrets include database passwords, storage connection strings, admin logins, service principals, etc.

## Why Credential Scanning ?
+ Including secrets in a project's source code is a significant risk, as it might make those secrets available to unwanted parties.
+ Spreading secrets in different places makes them harder to manage, access control, and revoke efficiently.
+ Secrets that are committed to source control are also harder to discard of, since they will persist in the source's history.
+ Coupling the project's code to its infrastructure and deployment specifics is limiting and considered a bad practice.

From a software design perspective, the code should be independent of the runtime configuration that will be used to run it, and that runtime configuration includes secrets.As such, there should be a clear boundary between code and secrets: secrets should be managed outside of the source code and *credential scanning* should be employed to ensure that this boundary is never violated.

## Types Of Credentials 
Different types of credentials my be hardcoded in the code and may be inadvertantly pushed to the git repository. These credetials may be :
+ Usernames and Passwords: Often used for accessing private repositories and services.
+ API Tokens: Many services, like GitHub, GitLab, or AWS, use API tokens for authentication and access control.
+ SSH Keys: Used for secure communication between repositories and servers.
+ OAuth Tokens: Used for integrating third-party services.
+ Access Tokens: Employed to control access to services and APIs.
+ Certificates: Used for SSL/TLS connections and code signing.

## When To Scan For Credentials
Ideally, credential scanning should be run as part of a developer's workflow (e.g. via a git pre-commit hook), however, to protect against developer error, credential scanning must also be enforced as part of the continuous integration process to ensure that no credentials ever get merged to a project's main branch.

## Credential Scanning Tools 
Credential scanning tools are used to identify and prevent the exposure of sensitive information, such as usernames, passwords, API keys, and other credentials, within source code, configuration files, or other repositories. Here are some popular credential scanning tools:

| **Tool** | **Description** |
| -------- | --------------- |
| **TruffleHog** | TruffleHog is a Python-based tool that scans Git repositories for high-severity security issues, including potential exposure of credentials. |
| **GitLeaks** | GitLeaks is an open-source tool designed to search through Git repositories for secrets and sensitive information. It supports various file types and allows you to customize the rules for finding credentials. |
| **RepoPeek** | RepoPeek is a lightweight Python tool that scans repositories on GitHub, GitLab, and Bitbucket to find sensitive information, including credentials, API keys, and more. |
| **GitGuardian** | GitGuardian is a commercial tool that specializes in scanning for sensitive data, secrets, and credentials in both public and private repositories. It supports various version control systems and integrates with CI/CD pipelines. |
| **Spectre** | Spectre is an open-source secrets scanner that supports various file types and can be integrated into CI/CD pipelines. It is designed to find secrets such as passwords, API keys, and other sensitive information. |
| **Hawkeye** | Hawkeye is a security tool that scans for secrets, API keys, and other sensitive information in source code repositories. It supports multiple file formats and can be integrated into CI workflows. |
| **Detect-Secrets** | *detect-secrets* is an open-source Python tool that scans code repositories, using regex-based patterns to identify and prevent the accidental inclusion of sensitive information like passwords or API keys. It's easily integrated into CI/CD pipelines and supports customizable configuration for reduced false positives. |

***

## Tool Comparison

| Feature                     | Gitleaks                           | detect-secrets                    | TruffleHog                        |
|-----------------------------|------------------------------------|-----------------------------------|-----------------------------------|
| **Purpose**                 | Scans git repositories for secrets | Searches for secrets in codebases | Searches for secrets in repositories |
| **Installation**            | Simple, binary installation        | Python package, pip install      | Python package, pip install      |
| **Configurability**         | Configurable through rulesets      | Configurable with regex patterns | Limited configuration options   |
| **Supported Repositories**  | Git repositories                   | Any code repository              | Git repositories                 |
| **Performance**             | Fast and lightweight               | Fast                              | Can be slow for large repositories |
| **Integration with CI/CD**  | Yes                                | Yes                               | Yes                               |
| **Custom Rulesets**         | Yes                                | Yes                               | Limited                           |
| **Ease of Use**             | Straightforward CLI usage          | Straightforward CLI usage         | Straightforward CLI usage        |
| **Output Formats**          | JSON, CSV, and others              | JSON, plain text                  | JSON, plain text                  |
| **Open Source**             | Yes, open-source                   | Yes, open-source                  | Yes, open-source                  |
| **Community Support**       | Active community                   | Active community                  | Limited                           |
***
## Tool Recommendation

**GitLeaks** is a simple but powerful tool for the purposes of credential scanning. Gitleaks offers a number of powerful features, including:
| **GitLeaks Feature** | **Description** |
| -------------------- | --------------- |
| Comprehensive scanning | Gitleaks scans not only your current codebase but also your entire repository history, ensuring that even secrets that were committed in the past can be identified. |
| Low false positive rate | Gitleaks uses a combination of heuristics and machine learning to identify potential secrets, resulting in a low false positive rate.
| Customizable rule-set | Gitleaks allows you to customize the rule-set to match your specific needs and environment. |
| Integration with CI/CD pipelines | Gitleaks can be integrated with popular CI/CD pipelines, such as GitHub Actions  to automatically scan your repositories for secrets whenever you push code changes.|

### GitLeaks vs Trivy 
 **Trivy** : Trivy is a comprehensive container scanning tool that focuses on identifying vulnerabilities in container images. It can scan container images for security vulnerabilities in both the operating system packages and application dependencies.

 Trivy too has a [secret scanning](https://aquasecurity.github.io/trivy/v0.27.1/docs/secret/scanning/) feature that is very much inspired from GitLeaks. If we plan a containerized deployment it might be prudent to use Trivy over Gitleaks however for non-containerized deployments GitLeaks can be effective as it is :

+ Lightweight
+ Less complicated as it has a narrower use case
+ Can be used at multiple stages i.e commit, pre-commit , repository scan , etc.
 
 ***

## Proof Of Concept : GitLeaks 

*Please refer the [GitLeaks Credential Scanning POC](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Design/02-%20Generic%20CI%20operation/Credentials%20Scanning/Credential%20Scanning%20via%20GitLeaks%20POC.md) for GitLeaks installtion process and proof of concept of credential scanning using GitLeaks.*

***
## Advantages 

| **Advantages of Credential Scanning Tools**                   |    **Description**                                   |
|-------------------------------------------------------------|---------------------------------------|
| **Security Improvement:** |  Prevent exposure of sensitive credentials in repositories & reduce attack surface and unauthorized access | 
| **Compliance and Regulatory Compliance:** | Ensure adherence to security standards and regulations & address industry-specific and regional compliance |
| **Early Detection of Vulnerabilities:** | Integrate with CI/CD for early detection in development & reduces time to remediate and mitigate vulnerabilities |      
| **Cost Savings:** | Prevent financial and reputational costs of security incidents & minimizes remediation costs through early detection |                        
| **Maintaining Trust:** | Build customer and user trust through commitment to security as we avoid fallout from data breaches |
***

## Best Practices 
Here are some best practices for effective credential scanning:

| **Best Practice**                   |    **Description**                                   |
|-------------------------------------------------------------|---------------------------------------|
| Regular Scanning | Implement regular and automated credential scanning across all code repositories, configuration files, and other relevant assets. |
| Integration with CI/CD Pipelines | Integrate credential scanning into your continuous integration/continuous deployment (CI/CD) pipelines. |
| Pattern-Based Scanning | Use pattern-based scanning tools that can recognize common formats of credentials, such as API keys, passwords, and access tokens. Customize these patterns to match your organization's specific credential formats. |
| Exclude Trusted Files and Paths | Define exclusion rules for trusted files and paths where credentials might be legitimately stored. This prevents unnecessary alerts and false positives, focusing the scan on areas of higher risk. |
| Secure Credential Storage | Encourage the use of secure credential storage solutions, such as vaults or key management services, rather than storing sensitive information directly in code or configuration files. |
| Audit Trails | Maintain audit trails for credential scanning activities. Keep records of scan results, actions taken, and any identified vulnerabilities. This information can be valuable for compliance purposes and continuous improvement. |
| Regular Updates |Keep your credential scanning tools and patterns up to date. Regularly update the tools to benefit from the latest security enhancements and ensure compatibility with evolving development practices. |

By implementing these best practices, organizations can significantly reduce the risk of credential leaks and enhance the overall security of their software development lifecycle.

***
## Conclusion  
In conclusion, credential scanning emerges as a fundamental practice in modern cybersecurity, offering a proactive approach to identifying and mitigating potential vulnerabilities within code repositories and configurations. By systematically searching for sensitive information like passwords and API keys, this practice serves as a critical line of defense against unauthorized access and data breaches. Integrated into the development lifecycle and bolstered by automated tools, credential scanning not only safeguards the integrity of systems but also fortifies organizations against evolving threats in the digital realm. In prioritizing the protection of sensitive data, credential scanning underscores its indispensable role in fostering a resilient and secure environment for software development and IT operations.

# Contact Information

| Name                 | Contact Information                                                                                     
|---------------------------------|------------------------------------------------------------|
| Aakash Tripathi                 |  aakash.tripathi.snaatak@mygurukulam.co
***
# References

|     Description                  | References  
| ---------------------------------| ------------------------------------------------------------------- |
| Credential Scanning | https://microsoft.github.io/code-with-engineering-playbook/continuous-integration/dev-sec-ops/secret-management/credential_scanning/ |
| GitLeaks |  https://akashchandwani.medium.com/what-is-gitleaks-and-how-to-use-it-a05f2fb5b034 | 
| detect-secrets | https://microsoft.github.io/code-with-engineering-playbook/continuous-integration/dev-sec-ops/secret-management/recipes/detect-secrets/ |
| Trivy | https://trunk.io/linters/security/trivy |

