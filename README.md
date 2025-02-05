# SIEM-lab

I’ll walk you through steps on how I set up a home lab for Elastic Stack Security Information and Event Management (SIEM) using the Elastic Web portal and a Kali Linux VM. I will generate security events on the Kali VM, set up an agent to forward data to the SIEM, and query and analyze the logs in the SIEM.

<h2>Overview </h2>

 1. Set up a free Elastic account.
 2. Install the Kali VM.
 3. Configure the Elastic Agent on the Linux VM to collect the logs and forward it to the SIEM.
 4. Generate security events on the Kali VM.
 5. Query to find the security events in the Elastic SIEM.
 6. Create a Dashboard to visualize security events.
 7. Create alerts for security events.


<h3>1.Set up an Elastic Account</h3>

Before we get started, we need to create a free account to set up a cloud Elastic instance that we can run the SIEM on. To do that, follow these steps:

 - Sign up for a free trial to use Elastic Cloud. 
 - Once you have an Elastic account, log in to the Elastic Cloud console.
 - Click on “Start your free trial.”
 - Click on the “Create Deployment” button and select “Elasticsearch” as the deployment type.
 - Choose a region and deployment size that fits your needs and click on “Create Deployment.”
 - Wait for the configuration to complete.
 - Once the deployment is ready, click “continue.”


<h3>2.Setting up the Linux VM</h3>

Next, we need to set up the Linux VM. You can use any Linux OS and virtualization software for this, but I’ll be using Kali Linux and Oracle VirtualBox.

 - Download the Kali Linux VM from the official Kali website.
 - Create a new VM with the Kali VM file in your preferred virtualization platform, such as VirtualBox or VMware.
 - Start the VM and follow the on-screen prompts to install Kali.
 - Once the installation is complete, log in to the Kali VM using the credentials “kali” for both the username and password.



<h3>3.Setting up the Agent to Collect Logs</h3>

An agent is a software program that is installed on a device, such as a server or an endpoint, to collect and send data to a centralized system for analysis and monitoring. In the context of Elastic SIEM, an agent is used to collect and forward security-related events from your endpoints to your Elastic SIEM instance.

To set up the agent to collect logs from your Kali VM and forward them to your Elastic SIEM instance, follow these steps:

 1. Log in to your Elastic SIEM instance and navigate to the Integrations page.

![1](https://github.com/user-attachments/assets/01bff0f9-6a16-4dab-a85f-a9b12dc843eb)

 2. Search for “Elastic Defend” and click on it to open the integration page.

![Screenshot 2025-02-05 190801](https://github.com/user-attachments/assets/b213dffe-877b-4212-9427-8377d895f1b1)

 3. Click on “Install Elastic Defend” and follow the instructions provided on the integration page to install the agent on your Kali VM.


 4. Paste that command from the elastic defend integration page into the Kali terminal (command line).


 5. Once the agent is installed, which can take a few minutes, you’ll see a message that says “Elastic Agent has been successfully installed.” It will automatically start collecting and forwarding logs to your Elastic SIEM instance, although it might take a few minutes for the logs to appear in the SIEM.


<h3>4.Generating Security Events on the Kali VM</h3>

To verify that the agent is working correctly, you can generate some security-related events on your Kali VM. To do this, we can use a tool like Nmap. Nmap (Network Mapper) is a free and open-source utility used for network exploration, management, and security auditing. It is designed to discover hosts and services on a computer network, thus creating a “map” of the network. Nmap can be used to scan hosts for open ports, determine the operating system and software running on the target system, and gather other information about the network.

<b>To run an Nmap scan, follow these steps:</b>

  - Install Nmap on the Linux VM if you’re not using Kali, Nmap already comes preinstalled in Kali. Open a new Terminal and run this command to install it: sudo apt-get install nmap.
  - Run a scan on Kali machine by running the command: sudo nmap <vm-ip>. You can also run a scan of your host machine if you place your Kali VM on a “bridged” network.


<h3>5.Querying for Security Events in the Elastic SIEM</h3>

Now that we have forwarded data from the Kali VM to the SIEM, we can start querying and analyzing the logs in the SIEM.

To do this, follow these steps:

  - Inside your Elastic Deployment, locate the “Logs” tab under “Observability” to view the logs from the Kali VM.

![4](https://github.com/user-attachments/assets/4d01c963-9e01-48a6-a74d-d27c5c583146)

  - In the search bar, enter a search query to filter the logs. For example, to search for all logs related to Nmap scans, enter the query: event.action:
“nmap_scan”.

  - The results of the search query will be displayed in the table below.


By generating and analyzing different types of security events in Elastic SIEM like the one above, or generating authentication failures by typing in the wrong password for a user or attempting SSH logins an incorrect password, you can gain a better understanding of how security incidents are detected, investigated, and responded to in real-world environments.


<h3>6.Create a Dashboard to Visualize the Events</h3>

You can also use the visualizations and dashboards in the SIEM app to analyze the logs and identify patterns or anomalies in the data. For example, you can create a simple dashboard that shows a count of security events over time.

Here’s how you can do that:

  - Navigate to the Elastic web portal at https://cloud.elastic.co/.
    
  - Click on the menu icon on the top-left, then under “Analytics” click on “Dashboards”.

  - Click on the “Create dashboard” button on the top right to create a new dashboard.

![Screenshot 2025-02-05 212525](https://github.com/user-attachments/assets/71ce0150-0b26-4e94-a148-28ac493265df)

  - Click on the “Create Visualization” button to add a new visualization to the dashboard.

![Screenshot 2025-02-05 212629](https://github.com/user-attachments/assets/127f9ffd-ebc1-48d3-9f65-0b17de916b04)

  - Select “Area” or “Line” as the visualization type, depending on your preference. This will create a chart that shows the count of events over time.

  - In the “Metrics” section of the visualization editor on the right, select “Count” as the vertical field type and “Timestamp” for the horizontal field. This will show the count of events over time.

![Screenshot 2025-02-05 212742](https://github.com/user-attachments/assets/4b220089-1860-4f67-babe-ab09c76117f6)

  - Click on the “Save” button to save the visualization.

![5](https://github.com/user-attachments/assets/be4b153f-d469-4212-984e-847e4c047565)


<h3>7.Create an Alert</h3>

In a SIEM, alerts are a crucial feature for detecting security incidents and responding to them in a timely manner. Alerts are created based on predefined rules or custom queries, and can be configured to trigger specific actions when certain conditions are met. In this task, we will walk through the steps of creating an alert in the Elastic SIEM instance to detect Nmap scans. By following these steps, you can create an alert that will monitor your logs for Nmap scan events and then notify you when they are detected.


  - Click on the menu icon on the top-left, then under “Security,” click on “Alerts.”
    
  - Click on “Manage rules” at the top right.

  - Click on the “Create new rule” button at the top right.

  - Under the “Define rule” section, select the “Custom query” option from the dropdown menu.

  - Under “Custom query”, set the conditions for the rule. You can use the following query to detect Nmap scan events.
   ` event.action:"nmap_scan"`

  - Under the “About rule” section, give your rule a name and a description.

  - Set the severity level for the alert, which can help you prioritize alerts based on their importance. Keep all the other default settings under “Schedule rule” and click “Continue.”


  - In the “Actions” section, select the action you want to take when the rule is triggered. You can choose to send an email notification, create a Slack message, or trigger a custom webhook.

  - Finally, click the “Create and enable rule” button to create the alert.


Once you’ve created the alert, it will monitor your logs for Nmap scan events. If an Nmap scan event is detected, the alert will be triggered and the selected action will be taken. You can view and manage your alerts on the “Alerts” section under “Security.”


<h2>Conclusion</h2>

In this guide, we have set up a home lab using Elastic SIEM and a Kali VM. We forwarded data from the Kali VM to the SIEM using the Elastic Beats agent, generated security events on the Kali VM using Nmap, and queried and analyzed the logs in the SIEM using the Elastic web interface. We also created a dashboard to visualize security events and then created an alert to detect security events.

This home lab provides a valuable environment for learning and practicing the skills necessary for effective security monitoring and incident response using Elastic SIEM. By following these steps, you can gain hands-on experience with using a SIEM and improve your security monitoring skills.

