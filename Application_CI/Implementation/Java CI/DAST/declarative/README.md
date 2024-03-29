# Declarative Pipeline Java DAST

<img width="668" alt="Screenshot 2024-02-20 at 5 00 24 PM" src="https://github.com/CodeOps-Hub/Documentation/assets/156056349/ca064fee-9fda-46b9-8073-9b3a4b87ad81">


|   Author        |  Created on   |  Version   | Last updated by  | Last edited on |
| --------------- | --------------| -----------|----------------- | -------------- |
| Vidhi Yadav |  20th February 2024  |  Version 1 | Vidhi Yadav | 20th Feb 2024    |

***
## Table of Contents
+ [Introduction](#Introduction)
+ [Declarative Pipeline](#Declarative-Pipeline)
+ [Flow Diagram](#Flow-Diagram)
+ [Pre-requisites](#Pre-requisites)
+ [Setup](#pipeline-setup)
+ [Conclusion](#Conclusion)
+ [Contact Information](#Contact-Information)
+ [Resources and References](#Resources-and-References)
  
***
## Introduction

[Dynamic Application Security Testing (DAST)](https://github.com/CodeOps-Hub/Documentation/blob/main/Application_CI/Implementation/GenericDoc/jenkinsPipeline.md) is an approach in the field of cybersecurity, dedicated to evaluating and enhancing the security posture of web applications. DAST operates dynamically during runtime, actively examining web applications in their functional state by simulating real-world attacks. Unlike static analysis, DAST assesses applications in their deployed environment, providing a comprehensive view of potential vulnerabilities and security weaknesses.

Visit this [link](https://github.com/CodeOps-Hub/Documentation/blob/main/Application_CI/Implementation/GenericDoc/jenkinsPipeline.md) to get comprehensive understanding of DAST


***
## Declarative Pipeline

Declarative Pipeline in Jenkins offers a simplified and structured approach for defining CI/CD pipelines, using a human-readable syntax with predefined sections like pipeline, stages, and agent. It's designed to be easy to read and maintain, making it suitable for users without strong scripting skills. While it may be less flexible in terms of allowing complex scripting logic, it is a newer and more concise way to define Jenkins pipeline.

**For more information visit the below document link:**

[\[ Reference Doc \]](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Implementation/GenericDoc/jenkinsPipeline.md )

***
## Flow Diagram

![Screenshot 2024-02-20 at 6 22 49 PM](https://github.com/CodeOps-Hub/Documentation/assets/156056349/8a77d270-e5d3-4620-b48d-0268359b27d8)

<img width="692" alt="Screenshot 2024-02-20 at 5 11 50 PM" src="https://github.com/CodeOps-Hub/Documentation/assets/156056349/910e9f0f-5be1-4eb1-972c-21d15a140df0">

***
## Pre-requisites

| Tool   | Description                          | 
|--------|--------------------------------------|
| OWASP ZAP (version: 2.14) | Tool required to perform DAST  | 
| Jenkins | CICD Tool                          |  
| JRE (Java runtime environment     | Zap is coded in Java, and its fundamental operations require a Java runtime environment for execution.    |

***
## Pipeline Setup

1. **Configure Jenkins Job**

<img width="916" alt="Screenshot 2024-02-20 at 5 02 54 PM" src="https://github.com/CodeOps-Hub/Documentation/assets/156056349/99a6b362-6fb3-427b-9023-07992bd48d08">

2. **Build Pipeline**


<img width="1243" alt="Screenshot 2024-02-20 at 2 33 23 PM" src="https://github.com/CodeOps-Hub/Documentation/assets/156056349/548c6ae8-bf02-4b68-8e4e-1061c094513c">

***
## Console Output
* Resultant output for ZAP attack

<img width="965" alt="Screenshot 2024-02-20 at 4 46 26 PM" src="https://github.com/CodeOps-Hub/Documentation/assets/156056349/a71d40f8-6fb3-49e5-b467-413b562b5464">

* HTML file reports generated as `result.html`

<img width="963" alt="Screenshot 2024-02-20 at 4 44 57 PM" src="https://github.com/CodeOps-Hub/Documentation/assets/156056349/fc69fe22-7e71-4374-8854-1be62891f0db">

* HTML Report can be found [**here**](https://github.com/CodeOps-Hub/Documentation/blob/main/Application_CI/Implementation/Java%20CI/DAST/declarative/ZAP%20Report.html)

<img width="1160" alt="Screenshot 2024-02-20 at 5 01 40 PM" src="https://github.com/CodeOps-Hub/Documentation/assets/156056349/1948e7bc-46ad-4012-a4ce-4f003d111b67">

***
## [Jenkinsfile](https://github.com/CodeOps-Hub/Jenkinsfile/blob/main/Declarative%20Pipeline/Java/DAST/Jenkinsfile)
```shell
pipeline {
    agent any

    environment {
        CURRENT_WORKSPACE = "${WORKSPACE}"
    }
    
    stages {
        stage('Clone Repository') {
            steps {
                // Clone the repository
                git branch: 'main', url: 'https://github.com/CodeOps-Hub/Salary-API.git'
            }
        }
        stage('Install ZAP') {
            steps {
                script {
                    // Download and install OWASP ZAP
                    sh 'wget https://github.com/zaproxy/zaproxy/releases/download/v2.14.0/ZAP_2.14.0_Linux.tar.gz'
                    sh 'tar -xf ZAP_2.14.0_Linux.tar.gz'
                }
            }
        }
        stage('Run Zap Scan') {
            steps {
                script {
                    sh "${CURRENT_WORKSPACE}/ZAP_2.14.0/zap.sh -cmd -port 8082 -quickurl http://174.129.170.198:8080/swagger-ui/index.html -quickout ${CURRENT_WORKSPACE}/results.html"
                }
            }
        }
        stage('Archive reports') {
            steps {
                // Archive ZAP scan report
                archiveArtifacts artifacts: '**/results.html'
            }
        }
    }
}
```

* For more comprehensive understanding of each step in the pipeline and detailed information, you can visit the following link: [Link to Documentation](https://github.com/CodeOps-Hub/Documentation/blob/main/Application_CI/Design/03-%20Java%20CI%20checks/DAST%20POC/README.md)

***
## Contact Information

| Name | Email address |
| ---- | ------------- |
| Vidhi Yadav | vidhi.yadhav.snaatak@mygurukulam.co |

***
## Resources and References

|  **Description** |   **Source** |
| ---------------- | ------------ |
| OWASP ZAP  | https://medium.com/globant/owasp-zap-integration-with-jenkins-795d65991404 |
| ZAP Official Documentation | https://www.zaproxy.org/ |
