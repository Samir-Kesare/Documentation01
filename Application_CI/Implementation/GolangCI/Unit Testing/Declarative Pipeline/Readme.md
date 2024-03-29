# Declarative Pipeline-Go Lang Unit Testing

  <img width="360" length="100" alt="Golang" src="https://github.com/avengers-p7/Documentation/assets/156056413/94c3280a-3e48-48bf-b2da-e1472a456262"> 

|   Author        |  Created on   |  Version   | Last updated by  | Last edited on |
| --------------- | --------------| -----------|----------------- | -------------- |
| Vishal Kumar Kesarwani |  09-02-2024  |  Version 1 | Vishal  | 09-02-2024    |

***
## Table of Contents
+ [Introduction](#Introduction)
+ [Why Declarative Pipeline](#Why-Declarative-Pipeline)
+ [Flow Diagram](#Flow-Diagram)
+ [Pre-requisites](#Pre-requisites)
+ [Setup of Unit Testing](#Setup-of-Unit-Testing)
+ [Jenkinsfile](#Jenkinsfile)
+ [Conclusion](#Conclusion)
+ [Contact Information](#Contact-Information)
+ [Resources and References](#Resources-and-References)
  
***
## Introduction

Declarative Pipeline is a streamlined way to define Jenkins pipelines using a structured syntax within a pipeline {} block. It offers simplicity, readability, and built-in directives for defining stages, steps, and more. It integrates well with the Jenkins UI, provides pipeline visualization, and supports pipeline templates for code reuse. It's ideal for teams looking for a straightforward approach to CI/CD pipeline configuration.

***
## Why Declarative Pipeline
| Aspect          | Description                                                                                               |
|-----------------|-----------------------------------------------------------------------------------------------------------|
| **Organization**    | Markdown tables organize pipeline stages, descriptions, and commands into neat columns for easier readability and understanding. |
| **Readability**     | Condenses verbose Declarative Pipeline syntax, particularly beneficial for complex pipelines, enhancing readability and comprehension. |
| **Documentation**   | Integrates pipeline configuration seamlessly into project documentation using Markdown, providing a comprehensive overview of CI/CD processes. |
| **Version Control** | Markdown files are version-controlled with tools like Git, enabling tracking of pipeline changes, revision history, and collaboration. |
| **Accessibility**   | Markdown files are viewable and editable with basic text editors or online Markdown editors, facilitating review and contribution by team members, including non-technical stakeholders. |
| **Presentation**    | Markdown files can be rendered into multiple formats, including HTML, PDF, and slideshows, enabling formatted documents or presentations for sharing and presentation purposes. |

***
## Flow Diagram  
![Screenshot from 2024-02-10 12-24-04](https://github.com/avengers-p7/Documentation/assets/156056413/a5324c1b-68c8-447c-9299-dcf28c6870d2)

***
## Pre-requisites
| **Pre-requisites** | **Version** |
| ------------------ | ----------- |
| Jenkins | 2.426.3 | 
| golang | 1.21.6 |

***
## Setup of Unit Testing
* Follow this document for Setup [**Cilck here**](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Implementation/GolangCI/Bug%20Analysis/Declarative%20Pipeline/Readme.md#Setup)

  <img width="760" length="100" alt="Golang" src="https://github.com/avengers-p7/Documentation/assets/156056413/44c961b0-24ff-43c0-8e2e-c5d4490dda5d"> 

* Console Output:
  
   <img width="760" length="100" alt="Golang" src="https://github.com/avengers-p7/Documentation/assets/156056413/5ee8690b-0e44-48c2-9e40-98b097509b9b"> 


> [!NOTE]
> **Changes**
> *  **Pipeline name**       **-**  `Unit _Testing_(golang_CI_Checks)_(Declarative)`
> *  **Jenkinsfile Path**    **-**  `Declarative Pipeline/golang/Unit Testing/Jenkinsfile`  

***

## HTML Report
 * Cilck [**here**](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Implementation/GolangCI/Unit%20Testing/Declarative%20Pipeline/Report.html)

***
## Jenkinsfile
  * [**Jenkinsfie**](https://github.com/avengers-p7/Jenkinsfile/blob/main/Declarative%20Pipeline/golang/Unit%20Testing/Jenkinsfile)
  ```shell
  
pipeline {
    agent any
    
    stages {
        stage('Installation Go') {
            steps {
                script {
                    // Update apt packages
                    sh 'sudo apt update'
                    // Install Go using snap
                    sh 'sudo snap install go --classic'
                    
                }
            }
        }
        stage('Clone Repository') {
            steps {
                // Clone the Git repository
                git branch: 'main', credentialsId: 'vishal-cred', url: 'https://github.com/OT-MICROSERVICES/employee-api.git'
            }
        }
        stage('Testing') {
            steps {
                script {
                    // Run go test and ignore errors
                    sh 'go test ./... || true'
                }
            }
        }
        stage('Generate HTML Report') {
            steps {
                script {
                    // Run gotest with specify the output format and generate HTML Report
                    sh 'go test ./... -coverprofile=coverage.out || true'
                    sh 'go tool cover -html=coverage.out -o coverage.html || true'
                    
                }
            }
        }
    }
}
```
***
## Conclusion

Declarative Pipeline simplifies Jenkins pipeline configuration, offering clarity, readability, and integration with Markdown tables. It enhances collaboration, version control, and accessibility while enabling easy documentation and presentation of CI/CD processes.

***
## Contact Information
| Name | Email address |
| ---- | ------------- |
| Vishal | vishal.kesarwani.snaatak@mygurukulam.co |
***
## Resources and References
|  **Description** |   **Source** |
| ---------------- | ------------ |
| About Jenkins Pipeline (Generic Document) | [Link](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Implementation/GenericDoc/jenkinsPipeline.md  ) |
| Flow Step for create pipeline | [Link](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Design/05-%20GoLang%20CI%20Checks/Unit%20Testing%20(GoLang%20CI%20Checks).md) |
| POC Generic Document | [Link](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Implementation/GenericDoc/pipelinePOC.md) |
| Setup Jenkins | [Link](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Implementation/GolangCI/Bug%20Analysis/Declarative%20Pipeline/Readme.md#Setup) |
| Jenkinsfile | [Link](https://github.com/avengers-p7/Jenkinsfile/blob/main/Declarative%20Pipeline/golang/Unit%20Testing/Jenkinsfile) |
| Scripted vs Declarative Pipelines | [Link](https://www.baeldung.com/ops/jenkins-scripted-vs-declarative-pipelines) |
| Unit Testing | [Link](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Design/03-%20Java%20CI%20checks/Intro-of-Unit-Testing.md) |

***
