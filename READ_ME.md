# DVWA Kubernetes Deployment

This project demonstrates how to deploy the Damn Vulnerable Web Application (DVWA) on a local Kubernetes cluster using Docker Desktop.

## Table of Contents

- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Deployment](#deployment)
- [Accessing DVWA](#accessing-dvwa)
- [Showcasing Attack Surfaces](#showcasing-attack-surfaces)
- [Contributing](#contributing)
- [Testing](#testing)
- [License](#license)
- [Credits](#credits)
- [Contact](#contact)

## Introduction

DVWA is a PHP/MySQL web application that is damn vulnerable. Its main goals are to aid security professionals in testing their skills and tools in a legal environment, help web developers understand the processes of securing web applications, and aid teachers/students in learning web application security in a controlled classroom environment.

This project will deploy DVWA on a Kubernetes cluster and showcase three attack surfaces as mentioned in its documentation.

## Prerequisites

Before you begin, ensure you have the following installed on your local machine:

- [Docker Desktop](https://www.docker.com/products/docker-desktop) (with Kubernetes enabled)
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- [Visual Studio Code](https://code.visualstudio.com/) (recommended)

## Installation

### Step 1: Clone the Repository

Clone this repository to your local machine:

```bash
git clone <repository-url>
cd <repository-directory>
  [25/06, 12:37 pm] ....: Step 2: Create Kubernetes YAML Files
Create the necessary Kubernetes manifest files in your project directory.
[25/06, 12:40 pm] ....: Apply Kubernetes Manifests
Apply the YAML files to create the DVWA deployment and service:
[25/06, 1:23 pm] ....: Step 3: Apply Kubernetes Manifests
Apply the YAML files to create the DVWA deployment and service:

code
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
[25/06, 1:25 pm] ....: Configuration
The provided YAML files include basic configurations for deploying DVWA. Modify the configurations as needed, such as updating environment variables, resource limits, or replica counts.

Deployment
Using Docker Desktop Kubernetes
Ensure Kubernetes is enabled in Docker Desktop settings.

code
kubectl config use-context docker-desktop
[25/06, 1:25 pm] ....: Apply the manifests:

code
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
[25/06, 1:25 pm] ....: Accessing DVWA
Port Forwarding (for Docker Desktop)
Use port forwarding to access the DVWA application:

                 

kubectl port-forward svc/dvwa-service 8080:80
Open your browser and navigate to http://localhost:8080 to access the DVWA application.
[25/06, 1:26 pm] ....: Prerequisites
DVWA Deployment: Ensure DVWA is deployed and accessible.
Browser: Use a web browser to interact with the DVWA interface.
1. SQL Injection
Objective: Exploit a SQL injection vulnerability to extract information from the database.

Steps:

Access DVWA: Open your browser and navigate to the DVWA application (e.g., http://localhost:<node_port>).
[25/06, 1:28 pm] ....: Login: Use the default credentials to log in.

Username: admin
Password: password
Set Security Level: Navigate to the DVWA Security tab and set the security level to Low.

Navigate to SQL Injection: Go to the SQL Injection section from the DVWA menu.

Perform SQL Injection:

In the input field (e.g., "User ID"), enter the following SQL injection payload:
 code
1' OR '1'='1
Click the Submit button.
Observe the Result: The application should return all user records from the database, indicating that the SQL injection was successful.

2. Cross-Site Scripting (XSS)
Objective: Execute a script in the context of another user's session.

Steps:

Navigate to XSS: Go to the XSS (Stored) section from the DVWA menu.

Perform XSS Attack:

In the "Name" input field, enter the following XSS payload:
html
code
<script>alert('XSS');</script>
Click the Submit button.
Observe the Result: The script should execute, displaying an alert dialog with the message "XSS". This indicates that the XSS attack was successful.

3. Command Injection
Objective: Execute arbitrary commands on the server.

Steps:

Navigate to Command Injection: Go to the Command Injection section from the DVWA menu.

Perform Command Injection:

In the input field (e.g., "Enter an IP address"), enter the following command injection payload:

code
127.0.0.1 && ls
Click the Submit button.
Observe the Result: The application should display the output of the ls command, listing the files and directories on the server, indicating that the command injection was successful.

Notes on Security and Ethical Hacking
Environment: Ensure you are performing these attacks in a controlled and legal environment, such as a local or private test network.
Cleanup: After demonstrating the attack vectors, clean up your Kubernetes resources to prevent unnecessary resource usage.

code
kubectl delete deployment dvwa
kubectl delete svc dvwa
Conclusion
By following these steps, you can demonstrate SQL Injection, XSS, and Command Injection vulnerabilities on the DVWA application deployed on your Kubernetes cluster. These demonstrations are crucial for understanding common web vulnerabilities and their potential impact. Always remember to conduct ethical hacking responsibly and within legal boundaries.
