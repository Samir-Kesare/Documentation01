# Declarative Pipeline For JAVA Bug Analysis


| **Author** | **Created On** | **Last Updated** | **Document Version** |
| ---------- | -------------- | ---------------- | -------------------- |
| **Parasharam Desai** | 07-02-2024 | 07-02-2024 | V1 |

***


# Table of Contents

1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Steps](#steps)
    - [Clone the repository](#1-clone-the-repository)
    - [Add Jenkinsfile](#2-add-jenkinsfile)
    - [Configure job](#3-configure-job)
    - [Evaluate Output](#4-evaluate-output)
4. [Conclusion](#conclusion)
5. [Contact Information](#contact-information)
6. [Resources and References](#resources-and-references)


***
# Introduction
Establishing a Java pipeline for bug analysis typically involves leveraging a CI/CD (Continuous Integration/Continuous Deployment) tool to automate the process of building, testing, and potentially deploying your Java application. Here we will be utilizing the Spotbugs plugin for bug scanning to ensure the quality and reliability of our codebase.
***
# Prerequisites
|    Tool                                   | Description                    |
|-------------------------------------------|----------------------------------|
| **Jenkins** | Enables Continuous Integration |
| **JDK17** | Required for compiling Jenkins and Spring Boot projects |
| **Maven** | Handles build automation and dependency management |
| **Spotbug** | Employed for bug analysis |


***
The Spotbugs plugin needs to be included in the pom.xml file.

            <plugin>
                  <groupId>com.github.spotbugs</groupId>
                  <artifactId>spotbugs-maven-plugin</artifactId>
                  <version>4.8.1.0</version>
                  <executions>
                      <execution>
                          <id>spotbugs-check</id>
                          <phase>verify</phase>
                          <goals>
                              <goal>check</goal>
                          </goals>
                      </execution>
                  </executions>
                  <dependencies>
                      <dependency>
                          <groupId>com.github.spotbugs</groupId>
                          <artifactId>spotbugs</artifactId>
                          <version>4.8.1</version>
                      </dependency>
                  </dependencies>
              </plugin>

              
Include the Spotbugs-maven-plugin within the reporting section. This ensures that running mvn site will generate the Spot Bugs report.

              <reporting>
                  <plugins>
                      <plugin>
                          <groupId>com.github.spotbugs</groupId>
                          <artifactId>spotbugs-maven-plugin</artifactId>
                          <version>4.8.1.0</version>
                      </plugin>
                  </plugins>
              </reporting>


# Steps
**1. Clone the repository:** You can clone the repository from GitHub - [https://github.com/Parasharam-Desai/salary-api.git](https://github.com/Parasharam-Desai/salary-api.git).
**2. Add Jenkinsfile:** Place the Jenkinsfile at the root level of the project with the provided code below. Ensure to modify the `credentialsId` as per the configuration in your Jenkins server.


                pipeline {
                    agent any
                    
                    tools {
                        maven 'mvn'
                    }
                    
                    stages {
                        stage("Git Checkout") {
                            steps {
                                script {
                                    git branch: 'main', url: 'https://github.com/Parasharam-Desai/salary-api.git'
                                }
                            }
                        }
                        
                        stage("Bug Analysis ") {
                            steps {
                                script {
                                    sh 'mvn compile'
                                    sh 'mvn spotbugs:spotbugs'
                                    sh 'mvn site'
                                }
                            }
                        }
                        
                        stage('Publish HTML Report') {
                            steps {
                                script {
                                    publishHTML([
                                        allowMissing: false,
                                        alwaysLinkToLastBuild: true,
                                        keepAll: true,
                                        reportDir: 'target/site',
                                        reportFiles: 'spotbugs.html',
                                        reportName: 'SpotBugs Report'
                                    ])
                                }
                            }
                        }
                    }
                }

**Description:**

- `mvn compile`: This command compiles the Java source code in the project.
- `mvn spotbugs:spotbugs`: This command executes the SpotBugs analysis using the SpotBugs Maven plugin. SpotBugs is a static analysis tool that identifies potential bugs in Java code.
- `mvn site`: The Maven site goal generates various reports, including a report for bug analysis.

3. **Configure job**: Configure the pipeline job in Jenkins and execute the pipeline. The Jenkinsfile is located at the root level of the project.



![image](https://github.com/Parasharam-Desai/working-repo/assets/156056709/1b3ac75a-b835-4d27-81b9-38cc50d2503c)


![image](https://github.com/Parasharam-Desai/working-repo/assets/156056709/46179379-ac84-4eb9-8d49-cb3bc6c193b3)


4. Evaluate Output: Based on the console output provided below, we can infer that there are a few bugs present.

![image](https://github.com/Parasharam-Desai/working-repo/assets/156056709/c27ed591-7cbe-4c52-a5a8-2e9dfbe485e2)

![image](https://github.com/Parasharam-Desai/working-repo/assets/156056709/a7d63f45-34fb-49e4-8612-a6058e857d98)

![image](https://github.com/Parasharam-Desai/working-repo/assets/156056709/dd07eea5-d7cf-4ac0-96b2-3ab1b70308f8)

# Conclusion
This pipeline will clone your source code repository, compile the project using Maven, and conduct bug scanning.


# Contact Information

|    Name                                   | Email Address                    |
|-------------------------------------------|----------------------------------|
| **[Parasharam Desai](https://github.com/Parasharam-Desai)** | parasharam.desai.snaatak@mygurukulam.co |

***
# Resources and References

|       **Description**                                   |           **References**                    |
|---------------------------------------------------------|-----------------------------------------------|
| Jenkins Pipeline     | [Jenkins Pipeline Documentation](https://www.jenkins.io/doc/book/pipeline/) |
| Using Spotbug Plugins                 | [Spotbugs Maven Plugin Documentation](https://spotbugs.readthedocs.io/en/latest/maven.html) |
| Guide to use SpotBugs           | [SpotBugs Maven Configuration Guide](https://github.com/find-sec-bugs/find-sec-bugs/wiki/Maven-configuration) |