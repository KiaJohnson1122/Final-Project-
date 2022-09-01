# Final-Project-


In this project, you will act as a security engineer supporting an organization's SOC infrastructure. The SOC analysts have noticed some discrepancies with alerting in the Kibana system and the manager has asked the security engineering team to investigate and confirm that newly created alerts are working.
If the alerts are working, you will then monitor live traffic on the wire to detect any abnormalities that aren't reflected in the alerting system. Then, you will report back your findings to the manager with appropriate analysis.

Unit Objectives

  
  


Days 1 and 2: Alert and Attacking Target 1

Configure alerts in Kibana
Attack a machine on the network.
Capture the flag on the victim machine.



Day 3: Wireshark Strikes Back

Capture network traffic
Investigate a number of suspicious activities
Collect corporate misuse evidence
Work in groups to create a presentation



Day 4: Final Group Presentations

Complete and submit group presentations
Submit an offensive red team analysis
Submit a defensive blue team analysis
Submit a network forensic analysis.





Lab Environment
Lab Details

In this unit, you will be using a new Web Vulns lab environment located in Windows Azure Lab Services. RDP into the Windows RDP host machine using the following credentials:

Username: azadmin

Password: p4ssw0rd*


This is a diagram of the network and the machines that will be used in this lab:

Open the Hyper-V Manager to access the nested machines:
ELK machine credentials: The same ELK setup that you created in Project 1. It holds the Kibana dashboards.

Username: vagrant

Password: vagrant

IP Address: 192.168.1.100


Kali: A standard Kali Linux machine for use in the penetration test on Day 1.

Username: root

Password: toor

IP Address: 192.168.1.90


Capstone: Filebeat and Metricbeat are installed and will forward logs to the ELK machine.

IP Address: 192.168.1.105

Please note that this VM is in the network solely for the purpose of testing alerts.



Target 1: Exposes a vulnerable WordPress server.

IP Address: 192.168.1.110


Target 2: Students should ignore Target 2 until they have completed all other parts of the project.
  

What to Be Aware Of:
It is common to encounter to experience the following issue:



If students encounter this error, explain that Kibana needs time to finish setting up. They should wait five to ten minutes and then try again.


If the issue is still not resolved, ask to students to log into the ELK machine using the machines credentials and run the following commands:


sudo su which will allow the student to become the root user.

docker container ls to find the name of the running docker container.

docker container stop <container-name> which will stop the docker container.

docker container start <container-name> which will start the docker container back up.



When setting alerts in Kibana to send log messages, those messages will not show in Kibana without additional configuration. Instead, the status of alerts can be viewed from the 'Watcher' page where the alerts are created.



Security+ Domains
This unit covers portions of the following domains on the Security+ exam:

1.0 Attacks, Threats, and Vulnerabilities
2.0 Architecture and Design
3.0 Implementation
4.0 Operations and Incident Response


  You are working as a Security Engineer for X-CORP, supporting the SOC infrastructure. The SOC analysts have noticed some discrepancies with alerting in the Kibana system and the manager has asked the Security Engineering team to investigate.
To start, your team needs to confirm that newly created alerts are working. Once the alerts are verified to be working, you will monitor live traffic on the wire to detect any abnormalities that aren't reflected in the alerting system.
You will then report back all your findings to both the SOC manager and the Engineering Manager with appropriate analysis.
You have two class days to complete this activity.

Instructions
Start by configuring new alerts in Kibana. Once configured, you will test them by attacking a system.
Open the Defensive Report Template and complete it as you progress through the activity.

Configuring Alerts
Complete the following to configure alerts in Kibana:


Access Kibana at 192.168.1.100:5601


Click on Management > License Management and enable the Kibana Premium Free Trial.


Click Management > Watcher > Create Alert > Create Threshold Alert


Implement three of the alerts you designed at the end of Project 2.


You can configure any alerts you'd like, but you are recommended to start with the following:


Excessive HTTP Errors

Select the packetbeat indice


WHEN count() GROUPED OVER top 5 'http.response.status_code' IS ABOVE 400 FOR THE LAST 5 minutes




HTTP Request Size Monitor

Select the packetbeat indice


WHEN sum() of http.request.bytes OVER all documents IS ABOVE 3500 FOR THE LAST 1 minute




CPU Usage Monitor

Select the metricbeat indice


WHEN max() OF system.process.cpu.total.pct OVER all documents IS ABOVE 0.5 FOR THE LAST 5 minutes





Viewing Logs Messages
There are a few way to to view these log messages and their associated data options.


First, you can see when alerts are firing directly from the Watcher screen.


As you attack Target 1, keep the watcher page open to view your alerts fire in real time.
  
---------------------------------------------------------------------------------------------------------------------------------------------  
  Attacking Target 1
Open the Offensive Report Template and complete it while you progress this activity.
You will need to run a few commands on Target 1 in order to ensure that it forwards logs to Kibana. Follow the steps below:

Open the Hyper-V Manager.
Connect to Target 1.
Log in with username vagrant and password tnargav.
Escalate to root with sudo -s.
Run /opt/setup.

This enables Filebeat, Metricbeat, and Packetbeat on the Target VM if they are not running already.
Now that you've configured alerts, you'll attack the Target 1 vulnerable VM on this network.
Note: Ignore the Target 2 machine at this time. If you complete the entire project with time to spare, ask your instructor for directions on attacking Target 2 and integrating it into your project.
Complete the following steps:


Scan the network to identify the IP addresses of Target 1.


Document all exposed ports and services.


Enumerate the WordPress site. One flag is discoverable after this step.


Hint: Look for the Users section in the output.



Use SSH to gain a user shell. Two flags can be discovered at this step.


Hint: Guess michael's password. What's the most obvious possible guess?



Find the MySQL database password.


Hint: Look for a wp-config.php file in /var/www/html.



Use the credentials to log into MySQL and dump WordPress user password hashes.


Crack password hashes with john.


Hint: Start by creating a wp_hashes.txt with Steven and Michael's hashes, formatted as follows


user1:$P$hashvalu3
user2:$P$hashvalu3




Secure a user shell as the user whose password you cracked.


Escalate to root. One flag can be discovered after this step.


Hint:  Check sudo privileges. Is there a python command you can use to escalate to sudo?



Try to complete all of these steps. However, you may move on after capturing only two of the four flags if you run out of time.

  
----------------------------------------------------------------------------------------------------------------------------------------------
  
  
  You are working as a Security Engineer for X-CORP, supporting the SOC infrastructure. The SOC analysts have noticed some discrepancies with alerting in the Kibana system and the manager has asked the Security Engineering team to investigate.
Yesterday, your team confirmed that newly created alerts are working. Today, you will monitor live traffic on the wire to detect any abnormalities that aren't reflected in the alerting system.
You are to report back all your findings to both the SOC manager and the Engineering Manager with appropriate analysis.
Fill out the Network Report Template as you progress through this activity.

Setup
You will use the Kali VM to analyze live traffic on the wire.
In order to get started, you will need to:

Connect to the Kali VM.
Open a terminal window and run the command systemctl start sniff.

This command uses tcpreplay to replay PCAPs in /opt/pcaps onto Kali’s eth0 interface.


Launch Wireshark and capture traffic on the eth0 interface.
After 15 minutes have passed, run the command systemctl stop sniff to stop the tcpreplay.

Please note that replaying the PCAPs will use up the CPU memory. You will need to stop this service in order to avoid performance issues with your virtual machine.


Save the capture to file. (This is an important step.)
Profile users' behavior from their packet data.

If you are unable to find some of the solutions, it is possible you did not allow Wireshark to capture traffic for long enough. To save time, feel free to use the following PCAP file below to answer the questions:

PCAP

Note: You will be dealing with live malware in this activity. Please make sure all work is done on Azure machines.

Instructions
Connect to your Kali VM, launch Wireshark, and begin capturing on the eth0 interface using the steps above. Let the capture run for at least fifteen minutes and then stop it. As your capture runs, read the following overview:


The Security team requested this analysis because they have evidence that people are misusing the network. Specifically, they've received tips about:

"Time thieves" spotted watching YouTube during work hours.
At least one Windows host infected with a virus.



A number of machines from foreign subnets are sending traffic to this network. Therefore, you will see many IP ranges in your capture.


Your task is to collect evidence confirming the Security team's intelligence.


Be sure to use display filters. In addition, be sure to record your work by adding comments to packets as you go.

For example, if you find a packet containing a username of interest, comment on the packet:



Record your answers in the following Google Doc. This file will be submitted as a deliverable at the end of the project. You must make a copy of this file in order to edit it.

Network Analysis Report Template


Time Thieves
At least two users on the network have been wasting time on YouTube. Usually, IT wouldn't pay much mind to this behavior, but it seems these people have created their own web server on the corporate network. So far, Security knows the following about these time thieves:

They have set up an Active Directory network.
They are constantly watching videos on YouTube.
Their IP addresses are somewhere in the range 10.6.12.0/24.

You must inspect your traffic capture to answer the following questions in your Network Report:


What is the domain name of the users' custom site?


What is the IP address of the Domain Controller (DC) of the AD network?


What is the name of the malware downloaded to the 10.6.12.203 machine?

Once you have found the file, export it to your Kali machine's desktop.



Upload the file to VirusTotal.com.


What kind of malware is this classified as?



Vulnerable Windows Machines
The Security team received reports of an infected Windows host on the network. They know the following:

Machines in the network live in the range 172.16.4.0/24.
The domain mind-hammer.net is associated with the infected computer.
The DC for this network lives at 172.16.4.4 and is named Mind-Hammer-DC.
The network has standard gateway and broadcast addresses.

Inspect your traffic to answer the following questions in your network report:


Find the following information about the infected Windows machine:

Host name
IP address
MAC address



What is the username of the Windows user whose computer is infected?


What are the IP addresses used in the actual infection traffic?


As a bonus, retrieve the desktop background of the Windows host.



