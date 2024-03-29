
# Proof of Concept (POC) for DAST

|   Authors        |  Created on   |  Version   | Last updated by | Last edited on |
| -----------------| --------------| -----------|---------------- | -------------- |
| Vidhi Yadav      | 25 Jan 2024   |     v1     | Vidhi Yadav     | 29 Jan 2024    |


<img width="475" alt="Screenshot 2024-02-04 at 1 43 55 PM" src="https://github.com/avengers-p7/Documentation/assets/156056349/0fb70c67-ed18-491e-87cb-7a54953ab6c2">

## Table of Contents
+ [Introduction](#Introduction)
+ [OWASP ZAP](#owasp-zap)
+ [Flow Diagram](#flow-diagram)
+ [Proof of Concept](#Pre-requisite)
+ [Conclusion](#conclusion)
+ [Contact Information](#contact-information)
+ [References](#references)

***
## Introduction 
* [Dynamic Application Security Testing (DAST)](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Design/02-%20Generic%20CI%20operation/DAST/Documentation/README.md) is an approach in the field of cybersecurity, dedicated to evaluating and enhancing the security posture of web applications. DAST operates dynamically during runtime, actively examining web applications in their functional state by simulating real-world attacks. Unlike static analysis, DAST assesses applications in their deployed environment, providing a comprehensive view of potential vulnerabilities and security weaknesses.


***
## OWASP ZAP
OWASP Zed Attack Proxy (ZAP) stands as a cornerstone in the realm of web application security, embodying the mission of the to fortify software against cyber threats. ZAP is an open-source and dynamic security testing tool designed to identify and mitigate vulnerabilities within web applications. Its robust capabilities span from intercepting and analyzing web traffic to actively scanning for security weaknesses, making it a great asset for security professionals, developers, and organizations committed to safeguarding their applications. 


***
## Flow Diagram

<img width="969" alt="Screenshot 2024-02-04 at 4 42 40 PM" src="https://github.com/avengers-p7/Documentation/assets/156056349/1505739f-60ea-46d4-967c-5327ab089cab">

***
## Advantages 
For a comprehensive explanation and a thorough exploration of the advantages, kindly refer to the following [link](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Design/02-%20Generic%20CI%20operation/DAST/Documentation/README.md).
***

## Proof of Concept (PoC)
### Pre-requisites
|   Tool        |  Description   |
| -----------------| --------------|
| OWASP ZAP (version: 2.14)     | Tool required to perform DAST   |   

|   Runtime         |  Description   |
| -----------------| --------------|
| JRE (Java runtime environment     | Zap is coded in Java, and its fundamental operations require a Java runtime environment for execution.    |


### 1. Setup ZAP

* Visit zap [website](https://www.zaproxy.org/docs/) and check the different installation packages for different OS

* Run the following command to download zap linux package using `wget`, then to extract the package.

```
wget https://github.com/zaproxy/zaproxy/releases/download/v2.14.0/ZAP_2.14.0_Linux.tar.gz
tar -xf ZAP_2.14.0_Linux.tar.gz
```

### 2. Run ZAP
* Now, to run our zap for analysis process.  Now running zap via zap.sh via -cmd or in daemon mode as it run the zap in Cli mode as shown below

```
<path to zap.sh> -port <port_no> -cmd -quickurl <url of website>
```

* <path to zap.sh> This is the executable file for OWASP ZAP
* The -port specifies the port on which ZAP will listen.
* -cmd indicates that the command should be executed in command-line mode.
* The -quickurl flag followed by the <url_of_website> parameter starts ZAP with the specified target URL.

### 3. Scanning API url

* The API and ZAP tool have been deployed on a virtual server. It has been ensured that the API is functioning correctly, and we can now proceed with the testing phase. For this process the following command was used:

```
/home/ubuntu/ZAP_2.14.0/zap.sh -cmd -quickurl http://34.69.125.44:8080/swagger-ui/index.html -port 8082 -quickout /home/ubuntu/zap_reports/results.html
```

### 4. Verify Reports 

* Navigate to the location where you saved your reports. Locate the generated `.html` reports. Ensure that vulnerabilities are correctly identified.

<img width="803" alt="Screenshot 2024-02-04 at 4 22 43 PM" src="https://github.com/avengers-p7/Documentation/assets/156056349/69a921ca-55c2-4640-9519-94538bf1bf94">

* The reports include information about the risk level and the number of alerts categorized. Following this overview, the reports provide specific details on each alert, presenting the alert name along with a concise description

<img width="1332" alt="Screenshot 2024-02-04 at 4 17 10 PM" src="https://github.com/avengers-p7/Documentation/assets/156056349/ab99ce71-b473-4632-acd2-09143560b548">

***
## Conclusion

* In conclusion, ZAP to check the security of our Java application, and it helped us find and fix some problems. But, it's important to know that keeping the application secure is an ongoing task. The information we got from this test is like a good starting point to make the application even more secure. It is advised to treat these findings seriously and implement appropriate remediation measures for overall security of our application.

* Since, security risks are always changing, it's really important to keep paying attention and regularly test and fix any issues in our applications. This ongoing effort is key to making sure our application stays strong and secure.

***
## Contact Information

|Vidhi Yadav                     | vidhi.yadhav.snaatak@mygurukulam.co                                                                                      
|---------------------------------|------------------------------------------------------------|

***
## References

| Title                                      | URL                                           |
|--------------------------------------------|-----------------------------------------------|
| OWASP documentation           | https://www.zaproxy.org/    |




