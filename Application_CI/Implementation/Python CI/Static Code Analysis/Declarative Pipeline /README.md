# Documentation of Declarative Pipeline for Static Code Analysis in Python

![image](https://github.com/avengers-p7/Documentation/assets/79625874/5419d5c8-ee87-4c28-9894-af831e8aba84)


***

| **Author** | **Created On** | **Last Updated** | **Document Version** |
| ---------- | -------------- | ---------------- | -------------------- |
| **Vikram Bisht** | **08-02-2024** | **08-02-2024** | **v1** |

***
# Table Of Contents

1. [Introduction](#Introduction)
2. [Pre-requisites](#Pre-requisites)
3. [Runtime Pre-requisites](#Runtime-Pre-requisites)
4. [Flow Diagram](#Flow-diagram)
5. [Configure Pipeline job](#Configure-Pipeline-job)
6. [Best Pratices](#Best-Pratices)
7. [Declarative Syntax](#Declarative-Syntax)
8. [Output or Job Result](#Output-or-Job-Result)
9. [Conclusion](#conclusion)
10. [Contact Information](#contact-information)
11. [References](#References)


# Introduction


In this documentation, we'll explore the integration of static code analysis into a Python code repository using the powerful Pylint tool within a Jenkins pipeline. Static code analysis is a crucial step in ensuring code quality by identifying potential issues, enforcing coding standards, and promoting best practices. Jenkins, a widely used automation server, allows us to automate this process through defined pipelines, providing a streamlined and consistent approach to code analysis.

Jenkins Declarative Pipeline is a feature of Jenkins, a popular open-source automation server. Declarative Pipeline is a way to define Jenkins Pipelines using a more structured and simplified syntax To know more about pipelines please follow this **[Reference Link](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Implementation/GenericDoc/jenkinsPipeline.md
)**

# Pre-requisites

| **Tool**   | **Description**            | 
| ---------- | -------------------------  | 
| Jenkins    | For continuous integration | 


# Runtime Pre-requisites

| **Tool**   | **Description**                                         | 
| ---------- | -------------------------                               | 
| Python3    | For python                                              | 
| Pylint     | It will help to do Static code analysis. on python code |


# Flow Diagram

![image](https://github.com/avengers-p7/Documentation/assets/79625874/2492a83d-bd29-4682-bb94-974fbaedca77)

# Configure Pipeline job

Set up Jenkins Pipeline job & Configure your pipeline using the detailed documentation provided in the following link:**

**[Reference Link](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Implementation/GenericDoc/pipelinePOC.md)**

# Best Pratices

By adhering to these best practices, you can establish a robust pipeline for static code analysis in Python projects using Jenkins Declarative Pipeline.

| **Aspect**                | **Description**                                         | 
| ----------                | -------------------------                               | 
| Pipeline Structure	    | Use a declarative pipeline structure to define stages and steps clearly. This provides better readability and maintainability. | 
| Code Checkout             | Implement a stage for checking out the code from the version control system (e.g., Git) to ensure the latest changes are analyzed. |
| Virtual Environment Creation    | Create a virtual environment to isolate dependencies and ensure consistent analysis. Utilize tools like venv or virtualenv for this purpose. |
| Dependency Installation    | Install project dependencies using pip or a dependency management tool. Use a requirements.txt file for specifying dependencies to maintain consistency. |
| Static Code Analysis    | Incorporate static code analysis tools like pylint, flake8, or bandit to analyze Python code for potential issues, adherence to coding standards, and security flaws. |
| Report Generation    | Generate reports from static code analysis tools to provide insights into code quality and potential improvements. |
| Artifact Archiving   | Archive generated reports and artifacts to ensure traceability and easy access for further analysis or reference. |
| Post-Build Actions   | Define post-build actions like sending notifications, triggering downstream jobs, or publishing reports to external systems for better integration and automation. | 



# Declarative Syntax
```
pipeline {
    agent any

    stages {
        stage('Code Checkout') {
            steps {
                git branch: 'main', credentialsId: 'Attendance-creds', url: 'https://github.com/OT-MICROSERVICES/attendance-api.git'
            }
        }

        stage('Create Virtual ENV') {
            steps {
                script {
                    sh 'python3 -m venv myenv'
                    sh '. myenv/bin/activate'
                }
            }
        }

        stage('Install dependencies') {
            steps {
                script {
                    sh 'python3 -m pip install -r requirements.txt'
                }
            }
        }

        stage('Static Code Analysis') {
            steps {
                script {
                    sh 'pylint router/ client/ models/ utils/ app.py | tee pylint.log'
                }
            }
        }
    }

    post {
        always {
            // Archive pylint reports
            archiveArtifacts artifacts: '**/pylint.log', allowEmptyArchive: true
        }
    }
}
```
# Output or Job Result

![image](https://github.com/avengers-p7/Documentation/assets/79625874/e2532ce3-7ad7-4867-8e23-22941f91a1f9)

If you want to see Detail Report please follow this **[Link](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Implementation/Python%20CI/Static%20Code%20Analysis/Scripted%20Pipeline/pylint.log)**

# Conclusion
This pipeline will do Static Code Analysis against a python code and provide you details report.

# Contact Information

|  Name                     |        	Email Address         |
| ------------              | --------------------------------|
| Vikram Bisht              |  Vikram.Bisht@opstree.com       |  

# References

|  Source                                                                                 |        Description      |
| ------------                                                                            | ----------------------- |
|  **[Link](https://pylint.readthedocs.io/en/stable/)**                                               | Pylint Documentation    |  
|**[Link](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Design/04-%20Python%20CI%20Checks/Static%20code%20analysis(Python%20CI%20Checks).md )**                  | Static Code Analysis Documentation    |
|  **[Link](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Implementation/Python%20CI/Static%20Code%20Analysis/Scripted%20Pipeline/pylint.log)**                                               | Detailed Output    |
|  **[Link](https://github.com/avengers-p7/Jenkinsfile/blob/main/Declarative%20Pipeline/Python/StaticCodeAnalysis/Jenkinsfile)**                                               | Jenkins File    | 
|  **[Link](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Implementation/GenericDoc/pipelinePOC.md)**   | How to Setup Jenkins Pipeline    |
