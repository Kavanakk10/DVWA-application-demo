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
- [conclusion](#conclusion) 

## Introduction

DVWA is a PHP/MySQL web application that is damn vulnerable. Its main goals are to aid security professionals in testing their skills and tools in a legal environment, help web developers understand the processes of securing web applications, and aid teachers/students in learning web application security in a controlled classroom environment.

This project will deploy DVWA on a Kubernetes cluster and showcase three attack surfaces as mentioned in its documentation.

## Prerequisites

Before you begin, ensure you have the following installed on your local machine:

- [Docker Desktop](https://www.docker.com/products/docker-desktop) (with Kubernetes enabled)
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- [Visual Studio Code](https://code.visualstudio.com/) (recommended)

## Installation

 Step 1: Clone the Repository

Clone this repository to your local machine


git clone <repository-url>
cd <repository-directory>

  Step 2: Create Kubernetes YAML Files
Create the necessary Kubernetes manifest files in your project directory.

 Apply Kubernetes Manifests
 
Apply the YAML files to create the DVWA deployment and service:

 Step 3: Apply Kubernetes Manifests
Apply the YAML files to create the DVWA deployment and service:


kubectl apply -f deployment.yaml

kubectl apply -f service.yaml

## Configuration

The provided YAML files include basic configurations for deploying DVWA. Modify the configurations as needed, such as updating environment variables, resource limits, or replica counts.


## Deployment

Using Docker Desktop Kubernetes. 
Ensure Kubernetes is enabled in Docker Desktop settings.


kubectl config use-context docker-desktop

 Apply the manifests:


kubectl apply -f deployment.yaml

kubectl apply -f service.yaml

## Accessing DVWA
Port Forwarding (for Docker Desktop)
Use port forwarding to access the DVWA application:

                 

kubectl port-forward svc/dvwa-service 8080:80

Open your browser and navigate to http://localhost:8080 to access the DVWA application.

Prerequisites
DVWA Deployment: Ensure DVWA is deployed and accessible.


## showcasing attack surfaces
Browser: Use a web browr to interact with the DVWA interface.
1. SQL Injection
Objective: Exploit a SQL injection vulnerability to extract information from the database.

Steps:

Access DVWA: Open your browser and navigate to the DVWA application (e.g., http://localhost:<node_port>).
 Login: Use the default credentials to log in.

Username: admin
Password: password

Set Security Level: Navigate to the DVWA Security tab and set the security level to Low.

Navigate to SQL Injection: Go to the SQL Injection section from the DVWA menu.

Perform SQL Injection:

In the input field (e.g., "User ID"), enter the following SQL injection payload:
 
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
<script>alert('XSS');</script>

Click the Submit button.
Observe the Result: The script should execute, displaying an alert dialog with the message "XSS". This indicates that the XSS attack was successful.

3. Command Injection
Objective: Execute arbitrary commands on the server.

Steps:

Navigate to Command Injection: Go to the Command Injection section from the DVWA menu.

Perform Command Injection:

In the input field (e.g., "Enter an IP address"), enter the following command injection payload:

127.0.0.1 && ls
Click the Submit button.

Observe the Result: The application should display the output of the ls command, listing the files and directories on the server, indicating that the command injection was successful.

Notes on Security and Ethical Hacking
Environment: Ensure you are performing these attacks in a controlled and legal environment, such as a local or private test network.

Cleanup: After demonstrating the attack vectors, clean up your Kubernetes resources to prevent unnecessary resource usage.


kubectl delete deployment dvwa
kubectl delete svc dvwa

## Conclusion
By following these steps, you can demonstrate SQL Injection, XSS, and Command Injection vulnerabilities on the DVWA application deployed on your Kubernetes cluster. 
