# System_Administration_Automation
## Project Overview 
This project helps automate the regular and time-consuming tasks of managing servers and systems hosted on Microsoft Azure. Instead of doing everything manually, it uses scripts to automatically create and manage virtual machines, check if important services are running smoothly, monitor disk space, and track any failed login attempts.

It collects all this information in one place using Azure's built-in monitoring tools, then generates easy-to-understand daily reports and shows this data on a simple web dashboard. When a problem happens, like a service keeps failing, it can automatically send alerts or emails to notify the right people.

Overall, this project makes system administration faster, less error-prone, and more organized by using automation, so admins and engineers can focus on more important work.

---
## Objective of the project 
This project is designed to: 
- Deploy infrastructure on azure cloud using automation scripts. 
- Service reliability & Auto-healing 
  * Pull server list from AD 
  * Document service status 
  * Escalate if the service fails to start on 3 consecutive checks.  
  * Failed logins  
- Disk space compliance 
  * Get the disk consumption details  
- Centralize Logging & Reporting 
  * Generate the Daily report  
  * Display the report on the App service 
- Policy Enforment 
  * Check metadata/tags (owner, Environment, service)
---
## Deliverables
- Automation scripts (PowerShell/ Bash) with modular structure. 
- Daily Report 
- Dashboard on Azure App Service 
- Weekly Compliance report (HTML/PDF) 

A GitHub repository containing: 
- PowerShell or CLI scripts for Azure VM Deployment 
- PowerShell scripts for Monitoring and Report generation 
- User documentation for how to use this project 
--- 
## Tech Stack
- Powershell/Bash- Report generation 
- Azure CLI / PowerShell – VM provisioning, automation and dashboard creation 
- Git & GitHub – Documentation and version control 
- Azure App service – Create app service and host dashboard
## Step 1: Deploy Infrastructure on Azure Cloud Using Automation Scripts

(Click here for the deployment Script)[]

### 1.1 Create Virtual Machines Using Script
- (Click here for bash script for creating 3 Ubuntu VMs)[]
Example script provisions VMs with required size, OS, networking, and tags.

1.2 Install Required Services on VMs
After VM creation, use Custom Script Extensions or remote execution to install applications:

Install Nginx web server for Linux VMs.
```
sudo apt-get update
sudo apt-get install -y nginx
sudo systemctl start nginx
sudo systemctl enable nginx
```

Install Apache web server.
```
sudo apt update
sudo apt install apache2 -y
sudo systemctl start apache2
sudo systemctl enable apache2
```
Install Mysql Database.
```
sudo apt-get update
sudo apt-get install -y mysql-server
sudo systemctl start mysql
sudo systemctl enable mysql
```
## Step-2 Service Reliability and Auto-Healing 
### Pull server list from AD 
To fetch all services irrespective of status 
```
systemctl list-units --type=service --all >> all_service.txt
```
(Click here for the script to escalate if the service fails to start on 3 consecutive checks)[]

## Step 3: Disk space compliance 
```
dh -f >> Diskcomsp.txt
```
## Step4:  Generate logging and reporting 
```
crontab -e  #to edit the cron file 
```
```
35 10 * * * /bin/bash/home/azure/allservises.sh >> home/azure/crone.daily   #It will generate the report everyday at 10:35
35 11 * * 1 /bin/bash/home/azure/allservises.sh >> home/azure/crone.daily  # It will generate the report every monday at 11:35
```
## Step 5:Zoombie process 
```
ps aux | grep 'Z'
```
## Project Summary
The project focused on developing an automated Linux service monitoring system using Bash scripting combined with scheduled execution via cron jobs. The core functionality involved:
- Periodically checking the status of critical services (e.g., Apache apache2).
- Maintaining a failure count for each monitored service by storing counts in temporary files.
- Logging alerts when a service fails consecutively beyond a configurable threshold.
- Collecting and logging additional system health information such as disk usage and zombie processes.
- Automating the monitoring process through cron jobs scheduled at specified times.
- Managing logs and outputs to designated files for audit and troubleshooting purposes

