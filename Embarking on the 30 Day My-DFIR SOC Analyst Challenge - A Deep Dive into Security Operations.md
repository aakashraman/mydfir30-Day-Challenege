
Welcome to my journey through the **30-Day MYDFIR SOC Analyst Challenge**! Whether you’re an aspiring SOC (Security Operations Center) analyst or an experienced cybersecurity professional looking to sharpen your skills, this challenge is designed to take you step by step through the core processes and tools that keep modern infrastructures secure. Over the course of the next 30 days, I’ll walk you through real-world scenarios, practical implementations, and hands-on troubleshooting techniques that are critical for maintaining and securing a robust SOC environment.

From setting up your first Elastic Stack, detecting brute force attacks, investigating threat actors, and establishing defense mechanisms to integrating powerful tools like Mythic C2 and Elastic Defend, this challenge covers it all. Each day focuses on a different aspect of SOC operations, progressively building on the skills you need to effectively monitor, analyze, and respond to cybersecurity threats.

Whether you’re deploying a firewall to safeguard against intrusions, configuring a ticketing system for incident management, or investigating complex alerts, you’ll find detailed, structured guides that will help you master the tools and techniques SOC analysts rely on every day.

**So, why take this journey with me?**

Because the cybersecurity landscape is constantly evolving, and keeping up with emerging threats requires more than just theoretical knowledge — it demands hands-on experience and continuous learning. This challenge will equip you with the skills to take control of your security environment and confidently tackle the real-world issues SOC analysts face every day.

Get ready to dive in, break down security concepts, and fortify your knowledge of SOC operations — one day at a time! Let’s get started!

###

### Day 0: What Awaits You

**Week 1: ELK Stack Essentials**

- Dive into the world of ELK Stack: Elasticsearch, Logstash, and Kibana.

- Learn how to set up and configure each component for optimal performance.

- Gain insights on ingesting and analyzing logs, including Sysmon, to extract valuable data.

**Week 2: Brute Force Attacks and Defense Strategies**

- Explore the mechanics of brute force attacks and the risks they pose to systems.

- Configure SSH and RDP servers to simulate potential vulnerabilities.

- Develop the skills to create alerts and dashboards, helping you detect and respond to threats efficiently.

**Week 3: Command and Control (C2) and Offensive Tactics**

- Delve into Command and Control (C2) frameworks with a spotlight on Mythic.

- Set up a C2 server and simulate real-world attacks on external servers.

- Learn how to identify and mitigate C2-based threats with hands-on exercises.

**Week 4: Ticketing Systems and Advanced Alert Investigation**

- Get practical experience with ticketing systems and their crucial role in security operations.

- Learn to integrate and configure these systems for smoother incident management.

- Sharpen your ability to investigate and handle high-priority security alerts with confidence.

I’m thrilled to embark on this 30-day challenge, which promises to sharpen my skills and deepen my understanding of digital forensics and incident response (DFIR). 

## Day 1: Creating a Logical Network Diagram with Draw.io

Welcome to Day 1 of the 30-Day MYDFIR SOC Analyst Challenge!, The first task today is to start with a crucial foundation: setting up a clear and organized logical network diagram. For this, I’ll be using **Draw.io** to visualize the components of our virtual environment, which is hosted on **Vultr Cloud**. This diagram will help me understand the architecture and flow of data throughout the environment as I progress through the challenge. This diagram is shown below and I will explain each of the components below.

***Security Architecture Logical Diagram***:

![[Pasted image 20241001115839.png]]
#### Virtual Private Cloud (VPC): The Backbone of the Network

- **Definition**: A Virtual Private Cloud (VPC) is a secure and isolated network segment within the cloud infrastructure provided by VULTR.
- **IP Range**: My VPC is defined by the IP range **172.31.0.1/24**, covering IPs from 172.31.0.1 to 172.31.0.254.
- **Subnet Mask**: A **255.255.255.0** subnet mask is in place, ensuring proper segmentation and efficient network management.
#### Core Servers: The Operational Units of the Setup

1. **Elastic & Kibana Server**:
   - **Role**: This server collects logs from various agents deployed across the environment.
   - **Interface**: It features a web-based GUI accessible to SOC Analysts for real-time data visualization and log analysis.

2. **Ticket Server**:
   - **Role**: The ticket server is responsible for generating alerts or tickets based on log analysis.
   - **Integration**: These alerts are forwarded to the SOC Analyst Laptop for immediate review and response.

3. **Ubuntu Server (SSH Enabled)**:
   - **Role**: Managed by the Fleet Server, this Ubuntu server helps handle logs and provide remote access via SSH for management purposes.

4. **Windows Server (RDP Enabled)**:
   - **Role**: Similar to the Ubuntu server, the Windows server is also managed by the Fleet Server and provides remote access using RDP.

5. **Fleet Server**:
   - **Role**: The Fleet Server centrally manages both the Ubuntu and Windows servers.
   - **Log Handling**: It ensures logs from both systems are forwarded to the Elastic & Kibana server for central analysis.

#### External Components: The Testing and Control Units

1. **Attacker Laptop (Kali Linux)**:
   - **Purpose**: This laptop is used for penetration testing and simulating attacks, providing a realistic threat scenario for the environment.
2. **C2 Server (Mythic)**:
   - **Role**: The C2 server simulates real-world Command and Control operations, managing compromised systems and executing attack scenarios.
#### Connectivity and Workflow

- The **Elastic & Kibana Server** is the central hub, aggregating logs and providing real-time insights through a web interface to the SOC Analyst Laptop.
- The **Ticket Server** generates actionable alerts, which are immediately relayed to the SOC Analyst for further investigation.
- The **Fleet Server** manages the Ubuntu and Windows servers, forwarding their logs for seamless monitoring.
- The **Attacker Laptop** and **C2 Server** play the role of external threats, adding a realistic edge to the simulation environment.
#### Purpose of this Setup

This setup is designed as a simulated Incident Response environment, providing a space to practice detecting, analyzing, and responding to security threats. At the core of this system is the **SOC Analyst Laptop**, which will serve as my primary control center for log analysis and alert management throughout the challenge. Each component is crucial for the overall learning experience, and this environment will evolve as I progress over the next 30 days.

---

**Summary**: Day 1 focused on laying the foundation of my SOC environment by creating a logical network diagram using **Draw.io**. This diagram gives me a comprehensive view of how each component—from the VPC to the external attacker laptop—fits into the overall architecture. This setup will be instrumental as I move forward with analyzing logs, managing alerts, and simulating real-world security scenarios.

### Day 2: Introduction to the ELK Stack

Welcome to Day 2 of the 30-Day MYDFIR SOC Analyst Challenge! Today's focus is to getting acquainted with the powerful ELK Stack. This suite of open-source tools—Elasticsearch, Logstash, and Kibana—forms the backbone of log data collection, search, analysis, and visualization. It plays a crucial role in monitoring, troubleshooting, and enhancing security analytics in IT and industrial settings.

#### What is the ELK Stack?

The **Elastic Stack** (commonly referred to as ELK) is a set of open-source tools developed by **Elastic**. It provides a robust platform for collecting, searching, analyzing, and visualizing logs from various sources and formats. The stack’s primary strength lies in its ability to offer deep insights for application and infrastructure monitoring, troubleshooting, and security analytics.

Let’s break down the individual components of the ELK Stack:

#### 1. Elasticsearch: The Search and Analytics Engine

The "E" in ELK stands for **Elasticsearch**, which serves as the core of the stack. It’s a highly scalable and flexible search and analytics engine, capable of processing vast amounts of data such as firewall logs, application logs, Windows event logs, and syslogs.

Key Features of Elasticsearch:
- **Real-Time Indexing and Search**: Elasticsearch enables fast data indexing and query performance, allowing for the real-time management and analysis of large datasets.
- **E-SQL (Elasticsearch SQL)**: It uses a SQL-like query language, enabling the execution of complex queries and aggregations in a structured way.
- **RESTful API**: Elasticsearch's REST API communicates through JSON, allowing for seamless integration with a variety of tools and platforms.

#### 2. Logstash: The Data Processing Pipeline

The "L" in ELK stands for **Logstash**, a crucial component for data ingestion and processing. Logstash collects, parses, filters, and forwards logs from different sources to Elasticsearch for indexing. This helps ensure that the data is clean, enriched, and structured before being analyzed.

- **Log Collection with Beats and Elastic Agent**: 
   - **Beats**: Lightweight data shippers that collect and send specific types of data to Elasticsearch. There are six main types:
     - **Filebeat**: For collecting log files from systems and applications.
     - **Metricbeat**: For collecting system and application performance metrics (CPU, memory, etc.).
     - **Packetbeat**: For monitoring network traffic.
     - **Winlogbeat**: For collecting Windows event logs.
     - **Auditbeat**: For gathering audit data related to security.
     - **Heartbeat**: For monitoring service and endpoint availability.
   - **Elastic Agent**: A unified agent that simplifies the deployment and management of data collection by combining the functionality of multiple Beats into one solution.

#### 3. Kibana: The Visualization and Exploration Interface

The "K" in ELK stands for **Kibana**, the user interface where data from Elasticsearch is visualized and analyzed. It allows users to create detailed dashboards, perform data exploration, and generate insights through a variety of tools.

Key Features of Kibana:
- **Kibana Lens**: A drag-and-drop interface for easily building custom visualizations.
- **Discover Tab**: Enables detailed data searches using ESQL for in-depth log exploration.
- **Machine Learning**: Detects anomalies and patterns in data, providing advanced analytics capabilities.
- **Elastic Maps**: Allows users to visualize geospatial data to analyze trends across locations.
- **Alerting and Reporting**: Facilitates the tracking of important metrics and events, with built-in alerting and reporting features for actionable insights.

#### Comparison: ELK Stack vs. Splunk

Though ELK and Splunk are both widely used for log management and analysis, their components can be mapped similarly:
- **Elasticsearch** parallels Splunk’s indexer.
- **Logstash** is equivalent to Splunk’s heavy forwarder.
- **Kibana** acts like Splunk’s search head and web interface.
- **Beats/Elastic Agent** are comparable to Splunk’s universal forwarder.

#### Benefits of Using the ELK Stack

- **Centralized Logging**: ELK offers a unified platform for managing logs, facilitating quick responses to security incidents and aiding in compliance.
- **Flexible Data Ingestion**: With the choice between Beats or Elastic Agent, data collection can be tailored to specific needs.
- **Advanced Visualizations**: Kibana allows for the creation of detailed, visually appealing dashboards for effective data presentation.
- **Scalability**: ELK can scale to fit growing environments, making it suitable for organizations of various sizes.
- **Ecosystem and Community**: With extensive community support and integrations, the ELK Stack continues to grow and evolve, offering additional features and functionality.

---

**Summary**: Day 2 has been all about understanding the **ELK Stack**—a critical toolset for managing and analyzing logs. The combination of **Elasticsearch** for search, **Logstash** for data processing, and **Kibana** for visualization makes this stack a powerful solution for IT monitoring, troubleshooting, and security analytics. As I progress through the challenge, the ELK Stack will become a cornerstone in handling large volumes of data efficiently and effectively.

### Day 3: Elasticsearch Installation and Setup

Welcome to Day 3 of the 30-Day MYDFIR SOC Analyst Challenge! Today, we will be taking a major step forward by setting up our own **Elasticsearch** instance, which will be essential in log management and analysis for our SOC tasks. By the end of this post, we will have Elasticsearch up and running on our virtual machine (VM), fully integrated with our Virtual Private Cloud (VPC). Let’s jump into it!

#### Step 1: Setting Up Your Virtual Private Cloud (VPC) on Vultr Cloud

To kick off, we’ll set up our Virtual Private Cloud (VPC) on Vultr. If you don’t have an account yet, head to the Vultr website and sign up—it's a simple process. Once your account is ready, follow these steps to create and configure your VPC:

1. **Navigate to the Products Section**: After logging into Vultr, go to the **Products** tab on the left-hand side. This is where all your cloud resources will be managed.
2. **Create a VPC**: Choose “Add Network” to set up a new VPC. This will allow you to create an isolated environment, crucial for security in your SOC operations.
3. **Configure the IP Range**: Use an IP range like **174.31.0.1/24** for your VPC.
4. **Add a Description**: Add a description for easy identification, such as “Elastic Search Deployment” or “SOC Analyst Environment.”

#### Step 2: Setting Up Your Virtual Machine (VM)

With your VPC in place, the next step is to launch a Virtual Machine (VM) within that environment:

1. **Choose the Instance Type**: Leave the default settings for instance type.
2. **Select the Location**: Ensure the location matches the one chosen for your VPC. This ensures that your VM operates in the same isolated network.
3. **Select the OS**: Choose **Ubuntu 22.04 LTS**, as it’s stable and well-suited for running Elasticsearch and other SOC tools.
4. **Choose a Plan**: Select the **80GB NVMe plan**, offering a good balance between storage and performance.
5. **Configure Features**: Uncheck default features and make sure to select your VPC for seamless network integration.
6. **Set the Hostname**: Name your VM something meaningful like "SOC-ElasticSearch" to easily identify it later.
7. **Deploy the VM**: Click **Deploy Now**, and your VM will be ready in a few moments.

#### Step 3: Booting Up and Accessing the VM

Once your VM is deployed, it’s time to boot it up and access it via SSH:

1. **Check VM Status**: In the Vultr dashboard, ensure your VM is up and running by checking its status.
2. **SSH into the VM**: Open your terminal (PowerShell or your preferred tool) and enter:  
   ```bash
   ssh root@<your-public-IP>
   ```
   Use the provided password to gain access to the VM’s command line.

#### Step 4: Installing Elasticsearch on the VM

Now that your VM is operational, it’s time to install Elasticsearch. Follow these steps:

1. **Update the System**: Run the following commands to update and upgrade your system packages:
   ```bash
   apt-get update
   apt-get upgrade
   ```
2. **Download Elasticsearch**: Fetch the latest Elasticsearch Debian package using wget:
   ```bash
   wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-x86_64.deb
   ```
3. **Install Elasticsearch**: Install the package using dpkg:
   ```bash
   dpkg -i elasticsearch-x86_64.deb
   ```

#### Step 5: Configuring Elasticsearch

Once Elasticsearch is installed, you’ll need to configure it for remote access:

1. **Edit the Configuration File**: Navigate to the configuration directory:
   ```bash
   cd /etc/elasticsearch
   nano elasticsearch.yml
   ```
2. **Update Network Settings**: In the file, change `network.host` from `127.0.0.1` to your VM’s public IP address. This allows external access.
3. **Set the HTTP Port**: Ensure the `http.port` is set to `9200`:
   ```yaml
   http.port: 9200
   ```
4. **Save and Exit**: Use `CTRL + X`, then press `Y` to save and exit the file.

#### Step 6: Securing Your Elasticsearch Instance

Securing Elasticsearch is crucial to prevent unauthorized access:

1. **Set Up Firewall Rules**: Navigate to the firewall section on Vultr:
   - **Create a Firewall Group**: Name it something like “30-Day-MYDFIR-SOC-Challenge.”
   - **Set Inbound Rules**: Restrict access to your IP for enhanced security.
   - **Apply Firewall Rules**: Apply the newly created firewall rules to your VM.

#### Step 7: Starting and Verifying Elasticsearch

The final step is to start the Elasticsearch service:

1. **Reload systemd Manager**:
   ```bash
   systemctl daemon-reload
   ```
2. **Enable Elasticsearch Service**:
   ```bash
   systemctl enable elasticsearch.service
   ```
3. **Start Elasticsearch**:
   ```bash
   systemctl start elasticsearch.service
   ```
4. **Verify Elasticsearch Status**:
   ```bash
   systemctl status elasticsearch.service
   ```

At this point, your Elasticsearch service should be running and ready to handle log data for SOC analysis!

---

**Summary**: Day 3 involved setting up a secure and functional Elasticsearch instance in a cloud environment using Vultr. By the end of this day, I’ve not only deployed a Virtual Private Cloud and Virtual Machine but also installed and configured Elasticsearch to start handling data indexing and search tasks. This foundational setup will be integral to my SOC analyst journey, especially as I continue building out the rest of the ELK Stack in the coming days.

### Day 4: Kibana Setup and Installation

Welcome to Day 4 of the 30-Day MYDFIR SOC Analyst Challenge! After successfully setting up Elasticsearch on Day 3, today we’ll configure **Kibana**, which provides the interface to interact with Elasticsearch data. This powerful visualization tool will allow us to explore logs, create dashboards, and set up alerts, all critical for SOC operations.

Let’s get started!

#### Step 1: Download and Install Kibana

To begin, we’ll install Kibana on the same VM where we set up Elasticsearch:

1. **Update Your System**: Make sure your system packages are up to date by running the following commands:
   ```bash
   apt-get update && apt-get upgrade
   ```
2. **Download Kibana**: Use `wget` to download the Kibana Debian package:
   ```bash
   wget https://artifacts.elastic.co/downloads/kibana/kibana-8.15.0-amd64.deb
   ```
3. **Install Kibana**: Once downloaded, install the package using `dpkg`:
   ```bash
   sudo dpkg -i kibana-8.15.0-amd64.deb
   ```

#### Step 2: Configure Kibana

After installation, we need to configure Kibana to work with our Elasticsearch instance:

1. **Edit the Configuration File**: Open the `kibana.yml` file for editing:
   ```bash
   nano /etc/kibana/kibana.yml
   ```
2. **Set the Server Port**: Uncomment and set the server port to 5601:
   ```yaml
   server.port: 5601
   ```
3. **Set the Server Host**: Replace `server.host` with your VM’s public IP address to allow external access:
   ```yaml
   server.host: "your-public-ip-address"
   ```
4. **Enable the Kibana Service**: Make sure Kibana starts on boot:
   ```bash
   sudo systemctl enable kibana.service
   ```
5. **Start the Kibana Service**: Start the Kibana service:
   ```bash
   sudo systemctl start kibana.service
   ```
6. **Verify the Service**: Check that Kibana is running:
   ```bash
   sudo systemctl status kibana.service
   ```

#### Step 3: Generate Elasticsearch Enrollment Token for Kibana

To secure the connection between Kibana and Elasticsearch, we need an enrollment token:

1. **Navigate to the Elasticsearch Bin Directory**:
   ```bash
   cd /usr/share/elasticsearch/bin
   ```
2. **Generate the Enrollment Token**:
   ```bash
   ./elasticsearch-create-enrollment-token --scope kibana
   ```
   Copy the generated token for later use.

#### Step 4: Accessing Kibana

With everything set up, let’s access Kibana through your web browser:

1. **Verify Services**: Ensure both Elasticsearch and Kibana services are running:
   ```bash
   sudo systemctl status elasticsearch.service
   sudo systemctl status kibana.service
   ```
2. **Access Kibana**: Open your browser and enter:
   ```
   http://your-public-ip-address:5601
   ```
3. **Firewall Configuration**: If you can’t access Kibana, it might be due to firewall settings. Allow traffic on port 5601:
   ```bash
   sudo ufw allow 5601
   ```
4. **Enter the Enrollment Token**: When prompted, paste the enrollment token you generated earlier.
5. **Verification Pin**: Generate the verification pin for Kibana:
   ```bash
   cd /usr/share/kibana/bin
   ./kibana-verification-code
   ```
   Enter this pin in Kibana to complete the setup.

#### Step 5: Setting Up Alerts in Kibana

Now that Kibana is running, we’ll set up the ability to manage alerts:

1. **Navigate to Alerts**: In Kibana, click on the **Alerts** section from the menu.
2. **Handle Encryption Keys**: Kibana may require encryption keys for alert management. You can generate them with the following:
   ```bash
   ./kibana-encryption-keys generate
   ```
   Store these keys in your token file and apply them to the Kibana keystore:
   ```bash
   ./kibana-keystore add xpack.encryptionSavedObjects.encryptionKey
   ./kibana-keystore add xpack.reporting.encryptionKey
   ./kibana-keystore add xpack.security.encryptionKey
   ```
3. **Restart Kibana**: To apply changes, restart Kibana:
   ```bash
   sudo systemctl restart kibana.service
   ```

#### Summary:

On Day 4, we successfully installed and configured **Kibana**, allowing us to visualize data from Elasticsearch and set up alerts for SOC operations. This installation is key for managing logs, creating dashboards, and generating actionable insights. Tomorrow, we’ll continue by setting up a Windows server for further SOC analysis tasks.

### Day 5: Setting Up a Windows Server with RDP

Welcome to Day 5 of the 30-Day MYDFIR SOC Analyst Challenge! Today, we’re taking a significant step by setting up a Windows Server with **Remote Desktop Protocol (RDP)**. This server will act as a target machine for various operations and will provide insight into how to deploy Windows instances in a cloud environment. Let’s dive into the setup.

#### Step 1: Deploying a New Windows Server on Vultr

To begin, we’ll deploy a new Windows Server using the Vultr platform:

1. **Log in to Vultr**: Start by logging into your **Vultr account**.
2. **Deploy a New Server**:
   - On the left-side menu, click on **Compute**.
   - Then, click the **Deploy +** button at the top-right corner.
3. **Choose Cloud Compute (Shared CPU)**:
   - For the server type, select **Cloud Compute - Shared CPU**. This is a cost-effective option suitable for our testing environment.
4. **Select the Location**:
   - Ensure the location matches that of your **VPC 2.0** for consistency in network configurations.
5. **Choose the Server Image**:
   - Select **Windows Standard 2022 x64** as the server operating system.
6. **Set the Storage**:
   - Opt for a **50GB SSD**, which provides ample storage for our tasks.
7. **Uncheck Additional Features**:
   - Do not select any additional features, particularly **VPC 2.0**. This ensures the Windows server is isolated, minimizing the risk of an attacker compromising the entire network if the server is breached.
8. **Set Hostname**:
   - Assign a recognizable name for your Windows machine, such as **SOC-WindowsServer**.
9. **Deploy the Server**:
   - Once all settings are configured, click **Deploy Now** to provision the server.

#### Step 2: Accessing the Windows Server via Console

After the server is deployed, we’ll access it through the web console:

1. **View Console**: Click **View Console** to open the web console for the Windows Server.
2. **Access the VM**:
   - Click the left arrow in the console and select **Show Extra Keys**.
   - Choose **Send Ctrl+Alt+Del** to unlock the server.
3. **Obtain the Password**:
   - Under **View Console** in Vultr, you can find and copy the automatically generated Windows Server password.
4. **Log in to the Server**:
   - In the console, go to the **Clipboard** option, paste the password, and press Enter to log in.

#### Step 3: Setting Up RDP Access

Now that we have access to the Windows Server, we can enable **Remote Desktop Protocol (RDP)** for easier management:

1. **Check if RDP Port (3389) is Open**:
   - Copy the public IP address of your server from Vultr.
   - On your local machine, open an **RDP client** (like Remote Desktop on Windows) and paste the public IP address.
   - Connect to the server using the credentials you obtained earlier. This allows you to access the server remotely instead of using the web console.

---

### Summary

On Day 5, we successfully deployed and configured a Windows Server with RDP access on Vultr. This setup is a key part of the challenge, as the Windows Server will serve as a target machine for various security tasks. With RDP enabled, we now have remote access to the server, preparing us for upcoming activities, including configuring the Fleet Server for endpoint management.

Tomorrow, we’ll take another step forward by exploring how to integrate the Windows Server into our SOC environment for monitoring and analysis. Stay tuned!

### Day 6: Introduction to Elastic Agent and Fleet Server

Welcome to Day 6 of the 30-Day MYDFIR SOC Analyst Challenge! After setting up our Windows Server with RDP yesterday, today’s focus is on introducing the **Elastic Agent** and **Fleet Server**, which are pivotal for managing multiple endpoints in a SOC environment. Before we dive into the technical setup, let’s explore a scenario to understand the importance of centralized management.

#### Scenario: Managing 100 Windows Endpoints

Imagine you’ve been tasked with installing Elastic Agents on **100 Windows machines** to monitor logs and metrics. You’re excited to start analyzing PowerShell logs in **Kibana**, only to realize that the agents were not configured to forward these logs to **Elasticsearch**. Now, you have to figure out how to fix this across all machines. Let’s explore three potential solutions:

1. **Manual Configuration on Each Machine**: 
   - This would involve visiting each machine and manually updating the Elastic Agent to forward logs. While this works, it’s inefficient and extremely time-consuming with 100 machines.

2. **Using Group Policy**: 
   - If the machines are part of a Windows domain, you can use Group Policy to push the new configuration. While faster than manual updates, this requires careful configuration to ensure all machines receive the updates correctly.

3. **Fleet-Managed Elastic Agents**: 
   - The most scalable and efficient option is using **Fleet** to centrally manage Elastic Agents. With Fleet, you can update the agent’s policy from a central dashboard, and all connected agents will receive the new configuration automatically. This method saves time, ensures consistency, and simplifies future updates.

#### What is the Elastic Agent?

The **Elastic Agent** is a unified solution for collecting logs, metrics, and security data. It simplifies the process by using **policies** that define what data to collect and where to send it (such as Elasticsearch or Logstash).

There are two ways to deploy Elastic Agents:

1. **Fleet-Managed Mode**: This mode allows you to centrally manage all agents via the Fleet UI in Kibana. Once the agent is installed, all configuration, updates, and policies are handled centrally. This is ideal for environments with numerous endpoints.

2. **Standalone Mode**: In this mode, agents are configured manually, and changes have to be made on each agent individually. This mode is best suited for small environments where centralized management isn't necessary.

In most cases, **Fleet-managed agents** are the better option, as they offer ease of use, scalability, and centralized control over policy management.

#### What is the Fleet Server?

The **Fleet Server** is the backbone of **Fleet-managed agents**. It connects Elastic Agents to the Fleet UI, allowing you to manage all your endpoints centrally. By deploying a Fleet Server, you can roll out updates, integrations, or new data collection policies across all endpoints from a single interface.

Without Fleet, managing agents on multiple endpoints becomes cumbersome, requiring manual configuration or Group Policy updates. Fleet simplifies this process by offering centralized management for all your agents.

---

### Summary

On Day 6, we explored the importance of **centralized management** for Elastic Agents and the role of the **Fleet Server** in simplifying this process. Fleet-managed agents offer a scalable, efficient solution for managing multiple endpoints in a SOC environment, saving time and reducing the potential for errors.

In the next session, we’ll dive into the process of installing Elastic Agents and setting up a Fleet Server to streamline endpoint management. Stay tuned!

### Day 7: Setting Up Elastic Agent and Fleet Server

Welcome to Day 7 of the 30-Day MYDFIR SOC Analyst Challenge! Today, we’re taking a critical step by setting up both the **Elastic Agent** and the **Fleet Server**. This setup will allow us to centrally manage our endpoints and monitor logs across our network, including the Windows server we deployed earlier.

By the end of this session, you'll have successfully installed the Elastic Agent on your Windows server and configured a Fleet Server to manage it. Let’s dive into the process!

---

#### Step 1: Creating the Fleet Server

The Fleet Server will act as the central management hub for all Elastic Agents. Here's how to set it up:

1. **Log in to Vultr**: Start by logging into your Vultr account.
2. **Deploy a New Server**:
   - Go to **Compute** and click **Deploy +** to create a new server.
   - Select **Optimized Cloud Compute — Dedicated CPU**.
   - Choose the same location as your Windows server to ensure they are within the same region.
   - For the OS, select **Ubuntu 22.04 LTS X64**.
   - Choose the **30GB NVMe storage and 1 vCPU** plan.
   - Under **VPC 2.0**, select the VPC you created earlier to keep it in the same isolated network.
   - Assign a meaningful **hostname**, such as **Fleet-Server**.
   - Click **Deploy Now** to create the server.

---

#### Step 2: Adding the Fleet Server to Fleet in Kibana

Now that the Fleet Server is created, let's add it to Fleet for centralized management:

1. **Access Kibana**:
   - Open your browser and navigate to your ELK server's Kibana interface:  
     ```
     http://<public-IP-of-ELK-server>:5601
     ```
   - In the left-side menu, scroll down and select **Fleet**.
2. **Add Fleet Server**:
   - Click **Add Fleet Server** and choose **Quick Start** (sufficient for this challenge).
   - Enter a name for your Fleet Server and the Fleet Server’s public IP in the **URL field**:  
     ```
     https://<public-IP-of-Fleet-Server>
     ```
   - Generate the **Fleet Server Policy**.
3. **Connect to Fleet Server**:
   - Log into the Fleet Server's terminal via **View Console** on Vultr.
   - Run the following commands to update the server:
     ```bash
     sudo apt update && sudo apt upgrade
     ```
   - Back in Kibana, copy the installation command generated for the Fleet Server (from the **Linux tier** section).
   - Paste the command into the Fleet Server terminal to install the Fleet Server.
4. **Troubleshoot Connectivity**:
   - If you encounter firewall errors, adjust the firewall rules in Vultr:
     - Go to **Network > Firewall**, find your firewall group, and add a new rule:  
       ```
       Port: 1-65535, Source: Custom, Public IP of Fleet Server
       ```
   - On the Fleet Server, allow traffic on **port 9200**:
     ```bash
     sudo ufw allow 9200
     ```
   - Re-run the installation command on the Fleet Server to complete the process.

---

#### Step 3: Enrolling the Elastic Agent on the Windows Server

Next, we’ll install and enroll the Elastic Agent on our Windows server:

1. **Create a Policy**:
   - In Kibana, go to **Fleet > Agents** and create a new policy named **mydfir-windows-policy**.
   - Check the box for **Collect system logs and metrics**.
2. **Install the Elastic Agent**:
   - In the **Windows tab**, copy the installation command.
   - Log into your Windows server via **RDP** or **Console** and open **PowerShell** with administrator privileges.
   - Paste the copied command into PowerShell and press **Enter** to install the Elastic Agent.
3. **Troubleshoot Connection Issues**:
   - If the agent is not connecting, ensure the Fleet Server can communicate with the Windows agent by allowing traffic on **port 8220**:
     ```bash
     sudo ufw allow 8220
     ```
   - In the Kibana Fleet settings, update the **Fleet Server URL** to use port **8220** instead of **443**.
   - Modify the Fleet Server policy command in PowerShell to use **port 8220**.

4. **Handling x509 Certificate Errors**:
   - If you encounter an x509 certificate error, bypass it by adding the `--insecure` flag to the policy command.

---

#### Step 4: Verifying Agent Enrollment

Once the Elastic Agent is installed:

1. **Check the Agents**:
   - In Kibana, go to **Fleet > Agents** and verify that both the Fleet Server and the Windows server are listed as active agents.
2. **Success!**:
   - You have successfully enrolled your Windows server into Fleet, and the Elastic Agent is now collecting logs and metrics from the system.

---

### Summary

On Day 7, we completed the critical task of setting up the **Elastic Agent** and **Fleet Server**. This centralized management setup will allow us to efficiently monitor logs and metrics from multiple endpoints without manually configuring each one. The Fleet Server simplifies endpoint management, saving time and ensuring all configurations are consistent.

Tomorrow, we’ll explore **Sysmon**, a powerful tool that provides deep insight into system activities on Windows machines, and integrate it with our setup for even more detailed monitoring. Stay tuned!

### Day 8: Introduction to Sysmon

Welcome to Day 8 of the 30-Day MYDFIR SOC Analyst Challenge! Today, we’re diving into **Sysmon (System Monitor)**, a powerful tool for gaining detailed visibility into endpoint activity. As SOC analysts, having comprehensive insights into what’s happening on our endpoints is critical, especially when it comes to tracking potential compromises. While Windows provides basic logging, it often falls short when it comes to critical events like process creations, network connections, and file modifications. This is where **Sysmon** comes in to fill the gap.

---

#### What is Sysmon?

**Sysmon** is a free tool from the **Sysinternals Suite** by Microsoft that provides advanced telemetry about system events, making it invaluable for detecting and investigating malicious activities. Sysmon allows you to monitor and log key activities, such as process creations, network connections, and file changes. It is highly customizable through configuration files, letting you define precisely which events to log.

---

#### Key Capabilities of Sysmon

1. **Process Creation Logging**: Sysmon logs every process creation, along with its command line, capturing both parent and child processes. This is particularly useful for identifying suspicious activities, such as malware execution.
  
2. **Process Hashing**: Sysmon records file hashes for processes, enabling you to use **OSINT** (Open-Source Intelligence) to analyze the file hash and gather additional context.

3. **Process GUID**: Sysmon assigns a **Globally Unique Identifier (GUID)** to each process, helping analysts correlate events across multiple logs for broader investigations into abnormal behavior or attacks.

4. **Network Connections**: Sysmon tracks network connections initiated by processes, logging the source and destination IPs, ports, and the initiating process. This is especially useful for identifying potential **Command and Control (C2)** traffic or unusual connections.  
   _Note: This feature is disabled by default and must be enabled via a configuration file._

---

#### Key Sysmon Event IDs for Investigations

Let’s look at some important Sysmon Event IDs that are frequently used in threat detection and analysis:

1. **Event ID 1: Process Creation**  
   This event logs the creation of new processes, along with their command lines and file hashes. If an attacker executes malware, Sysmon will capture it with Event ID 1, giving you crucial information for investigation.

2. **Event ID 3: Network Connections**  
   Once enabled, this event logs network connections initiated by processes, tracking both the source and destination IP addresses and ports. This is useful for identifying suspicious network traffic, such as unexpected C2 connections.

3. **Event IDs 6/7/8: Driver/Image Load & Create Remote Thread**  
   These events can reveal attempts at **defense evasion techniques**, such as process injection, where malicious code is injected into legitimate processes. Although these events can be noisy, Sysmon’s **Process GUID** helps filter relevant events.

4. **Event ID 10: Process Access**  
   This event logs access to other processes, which is useful for detecting potential credential access attacks. For example, monitoring access to **lsass.exe** can help detect attempts to steal credentials from memory.

5. **Event ID 22: DNS Query**  
   This event logs DNS queries made by the system. Suspicious DNS activity, such as queries to domains generated by a **Domain Generation Algorithm (DGA)**, can indicate compromise. By following the **Process GUID**, you can trace the source of the DNS query.

---

#### Why Sysmon is Essential for Endpoint Monitoring

Sysmon gives analysts a deep level of insight into endpoint activity that basic Windows logs don’t provide. Its **granularity** and **flexibility** make it a powerful tool for detecting abnormal behavior, such as:
- Malware execution
- Unusual network traffic
- Credential dumping attempts
- Process injections

By customizing Sysmon with configuration files, you can tailor which events are logged, focusing on what matters most to your environment.

---

### Summary

On Day 8, we explored **Sysmon (System Monitor)**, a powerful tool from the **Sysinternals Suite** designed to provide detailed telemetry on endpoint activity. Sysmon goes beyond the basic Windows logging, offering deep insights into process creation, network connections, file changes, and more through customizable configuration files. Key event IDs such as **Process Creation (ID 1)**, **Network Connections (ID 3)**, and **DNS Queries (ID 22)** were highlighted as essential for detecting and investigating malicious activity. 

Sysmon’s flexibility, combined with the use of **process hashing** and **Process GUIDs**, makes it an invaluable tool for tracking threats, tracing suspicious activity, and identifying compromise attempts in real time. Tomorrow, we’ll take the next step by installing Sysmon on our Windows server and configuring it to start capturing these critical logs.

This foundational knowledge will help elevate your endpoint monitoring capabilities and take your threat detection to the next level.

### Day 9: Sysmon Installation

Welcome to Day 9 of the 30-Day MYDFIR SOC Analyst Challenge! Today, we’re installing and configuring **Sysmon** on our Windows server, which we deployed on Day 5. By the end of this task, Sysmon will be actively generating logs, helping us monitor key system events for security insights.

---

#### Step 1: Prepare Your Environment

1. **Log in to Your Windows Server**:
   - Go to your **Vultr account** and select the Windows server you set up on Day 5.
   - Copy the **public IP address** of the Windows server.
   - On your local machine, open **Remote Desktop Connection** and enter the public IP.
   - When prompted, log in with the **Administrator** username and the associated password.

---

#### Step 2: Download and Extract Sysmon in the VM

1. **Download Sysmon**:
   - On the Windows server, open a browser and search for “**Sysmon**.”
   - Go to the official **Microsoft Sysmon** download page.
   - Download the Sysmon ZIP file.
2. **Extract Sysmon**:
   - Once downloaded, unzip the file. You should see three files: **Sysmon.exe**, **Sysmon64.exe**, and **EULA.txt**.

---

#### Step 3: Download the Sysmon Configuration File in the VM

1. **Search for Sysmon Configuration**:
   - Search for “**Olaf’s Sysmon configuration**” in your browser inside the VM.
   - The first link should take you to **Olaf Hartong’s Sysmon Modular repository** on GitHub.
2. **Download the Config File**:
   - Scroll down to find **sysmonconfig.xml**.
   - Click on it, then click **Raw** on the right-hand side.
   - Right-click the page, select **Save As**, and save the file as **sysmonconfig.xml** in the same folder where you extracted Sysmon.

---

#### Step 4: Install Sysmon

1. **Open PowerShell as Administrator**:
   - Search for **PowerShell**, right-click it, and select **Run as administrator**.
2. **Navigate to the Sysmon Folder**:
   - Copy the **path** of the Sysmon folder from the file explorer address bar.
   - In PowerShell, type `cd ` and paste the folder path, then press **Enter**.
   - Type `dir` to confirm you’re in the correct directory.
3. **Install Sysmon**:
   - Run the following command:
     ```bash
     .\Sysmon64.exe -i sysmonconfig.xml
     ```
   - A license dialog will appear. Click **Agree** to proceed.
   - Sysmon will now install and configure itself based on the **sysmonconfig.xml** file.

---

#### Step 5: Verify Sysmon Installation

1. **Check the Sysmon Service**:
   - Open the **Services** application by searching for “Services.”
   - Press **S** to jump to services starting with S, and scroll down to verify that **Sysmon** is listed and running.
2. **Verify Sysmon Logs in Event Viewer**:
   - Open **Event Viewer**.
   - Navigate to **Application and Services Logs > Microsoft > Windows**.
   - Scroll down to find **Sysmon**, expand it, and click on **Operational**.
   - You should see logs, including **Event ID 3** for network connection monitoring, confirming that Sysmon is capturing events.

---

### Summary

We’ve successfully installed and configured **Sysmon** on your Windows server. Sysmon is now actively generating logs that capture key events like process creation, network connections, and more. These logs will give you valuable insights into system activities, helping to monitor and detect suspicious behaviors.

Tomorrow, we’ll integrate Sysmon logs with our Elasticsearch instance to streamline our monitoring and analysis processes. Stay tuned for more advanced insights!

### Day 10: Ingesting Data into Elasticsearch

Welcome to Day 10 of the 30-Day MYDFIR SOC Analyst Challenge! Today, we’re focusing on how to ingest **Sysmon** and **Microsoft Defender** event logs from your Windows server into your **Elasticsearch** instance. This process will ensure that critical security logs are centralized for easier analysis and monitoring.

---

#### Step 1: Start the Machines

1. **Start your Windows and ELK Servers**:
   - Log in to your **ELK server** and navigate to the homepage.
   - Click the big blue **Add Integrations** button to access various integration options.

---

#### Step 2: Set Up Sysmon Log Ingestion

1. **Search for “Custom Windows Event Logs”**:
   - This integration allows you to ingest events from any Windows event log channel.
2. **Begin the Setup**:
   - Click **Add Custom Event Logs** and fill in a name and description for the integration.
3. **Specify the Sysmon Event Log Channel**:
   - On your **Windows server**, open **Event Viewer** and go to **Applications & Services Logs > Microsoft > Windows > Sysmon**.
   - Right-click **Operational**, select **Properties**, and copy the full channel name.
   - Paste this channel name into the integration’s setup on your ELK server.
4. **Apply to Agent Policy**:
   - Under "Where to add this integration?", select your existing Windows agent policy (created on Day 7).
   - Click **Save & Continue**, then **Save & Deploy Changes**.

---

#### Step 3: Set Up Microsoft Defender Log Ingestion

1. **Add Custom Event Logs Again**:
   - Go through the same steps as Sysmon, but this time focus on **Windows Defender** logs.
2. **Set the Defender Event Log Channel**:
   - On your Windows server, navigate to **Event Viewer > Applications & Services Logs > Microsoft > Windows > Windows Defender**.
   - Right-click **Operational**, copy the full channel name, and paste it into the integration’s setup.
3. **Advanced Options**:
   - You can include or exclude specific event IDs by entering them in the field. For Defender, commonly tracked event IDs include **1116**, **117**, and **5001**.
   - Apply the changes to the same Windows agent policy and save.

---

#### Step 4: Verify the Logs

1. **Check Logs in Elasticsearch**:
   - Go to **Discover** in the ELK interface, and type `sysmon` in the search bar.
   - If logs don’t appear right away, troubleshoot by:
     - Returning to **Integrations** and looking for **winlog.event_id** values.
     - Copying one of the event IDs and searching for it in **Discover**.
   - After a few minutes, logs from both **Sysmon** and **Microsoft Defender** should begin appearing.

---

#### Step 5: Troubleshooting Steps

1. **Ensure Integrations Are Healthy**:
   - Go to **Fleet**, click on the Windows agent, and ensure both integrations are in a healthy state.
2. **Restart the Elastic Agent**:
   - If issues persist, restart the **Elastic Agent** on your Windows server by opening **Services**, finding **Elastic Agent**, right-clicking, and selecting **Restart**.
3. **Check Firewall Settings**:
   - On your ELK server, ensure that port **9200** is open for incoming connections.
   - In Vultr, allow TCP traffic on **port 9200** from relevant sources.

---

#### Step 6: Final Check and Log Viewing

1. **Check for New Data in Elasticsearch**:
   - Return to **Discover** in Elasticsearch and click **Check for New Data**.
   - You should now see logs from both **Sysmon** and **Microsoft Defender**.
2. **Review Event Details**:
   - Click on any event to view detailed information, including the event provider, which will either be **Sysmon** or **Microsoft Windows Defender**.

---

### Summary

On Day 10, we successfully ingested **Sysmon** and **Microsoft Defender** logs into our **Elasticsearch** instance, centralizing these logs for better visibility and monitoring. This is a crucial step in gaining insights into your Windows server’s activity and detecting potential security threats.

Tomorrow, we’ll explore common attack patterns and learn how to use these logs to detect malicious behavior, further enhancing your SOC analyst skills.

### Day 11: A Comprehensive Guide to Brute Force Attacks

Welcome to Day 11 of the 30-Day MYDFIR SOC Analyst Challenge! Today, we’ll explore **brute force attacks**, a common method used by attackers to break into systems by guessing passwords. We’ll discuss the different types of brute force attacks, the tools attackers commonly use, and effective ways to defend yourself against these attacks.

---

#### What is a Brute Force Attack?

A brute force attack is similar to trying to guess the combination of a locked suitcase by attempting every possible code until it opens. In the digital world, this means systematically trying every possible combination of passwords to gain access to an account. These attacks are automated and can target systems like email accounts, websites, or any online service that requires login credentials.

For instance, if you see multiple failed login attempts from different IP addresses in your account's login logs, it could be a sign that someone is trying to brute force their way into your account. While many attacks fail, weak passwords make it easier for attackers to eventually succeed.

---

#### Types of Brute Force Attacks

Brute force attacks can vary in approach. Here are the most common types:

1. **Simple Brute Force Attack**:
   - This involves trying every possible combination of characters in a password, one by one. The attack is relentless and fully automated, starting from “0000” and going all the way to “9999” or higher, depending on the complexity.

2. **Dictionary Attack**:
   - Instead of trying random combinations, attackers use a predefined list of common passwords or phrases, often sourced from leaked password databases. Since many users reuse simple passwords, this method can be more efficient than a simple brute force attack.

3. **Credential Stuffing**:
   - In this attack, hackers use known usernames and passwords obtained from data breaches and attempt to use them on other services. Since many people reuse passwords across platforms, credential stuffing is highly effective.

---

#### How to Protect Yourself from Brute Force Attacks

Brute force attacks are preventable if you use the right security practices. Here are three key methods to defend yourself:

1. **Use Strong Passwords or Passphrases**:
   - Long and complex passwords make brute force attacks significantly more difficult. Aim for at least 15 characters, mixing upper and lowercase letters, numbers, and symbols. Using a password manager can help you create and store these complex passwords.

2. **Enable Multi-Factor Authentication (MFA)**:
   - MFA adds an extra layer of protection to your accounts by requiring a second piece of information (like a code sent to your phone) in addition to your password. This ensures that even if someone guesses your password, they cannot access your account without the second authentication factor.

3. **Stay Vigilant**:
   - Be cautious of phishing attempts and regularly monitor your accounts for any unusual activity. Use services like **HaveIBeenPwned** to check if your email address has been involved in a data breach, and if so, change your passwords immediately.

---

#### Common Tools Used in Brute Force Attacks

Brute force attacks are often carried out using popular tools, especially those available in penetration testing distributions like **Kali Linux**. Here are three commonly used tools:

1. **Hydra**:
   - A fast and flexible brute force tool that supports a wide range of protocols, including SSH, FTP, and HTTP. It is commonly used for password cracking on remote systems.

2. **Hashcat**:
   - Known for its speed and efficiency, Hashcat is a powerful password-cracking tool that leverages GPUs to perform brute force and dictionary attacks. It's ideal for cracking hashed passwords.

3. **John the Ripper**:
   - A widely used open-source tool for password cracking, often applied to test the strength of passwords in local files, like Unix shadow files.

While there are many other tools for brute force attacks, these three are often the starting point for those learning about ethical hacking. Always ensure that you only use them on systems you own or have explicit permission to test.

---

### Summary

On Day 11, we explored **brute force attacks**, their various types, and how attackers leverage these methods to crack passwords. We also discussed the tools commonly used for brute force attacks, such as **Hydra**, **Hashcat**, and **John the Ripper**, and outlined best practices to defend yourself, including using strong passwords, enabling multi-factor authentication, and maintaining vigilance. 

Tomorrow, we’ll take things further by setting up an SSH server in the cloud, allowing us to monitor brute force attacks in real-time and deepen our understanding of how they occur in practical scenarios.

### Day 12: Setting Up an Ubuntu Server and Reviewing Authentication Logs

Welcome to Day 12 of the 30-Day MYDFIR SOC Analyst Challenge! Today, we’ll be setting up an **Ubuntu server** with **SSH** enabled in the cloud. Once the server is up and running, we'll review the **authentication logs** to monitor login attempts and detect potential brute force attacks. This exercise will help you gain visibility into login activities, providing a hands-on understanding of how to monitor your server in real-time.

---

#### Step 1: Setting Up Our Virtual Machine (VM)

1. **Log in to Vultr**:
   - Go to your **Vultr account** and navigate to the **Compute** section to deploy a new virtual machine.
2. **Choose the Server Configuration**:
   - Select an **Optimized Shared CPU** instance.
   - Choose the same **location** you used for your VPC 2.0 setup to ensure the VM stays within the same network region for consistency.
3. **Select the OS and Plan**:
   - Choose **Ubuntu 22.04 LTS** as the operating system.
   - Opt for a **25GB NVMe, 1GB RAM, 1 CPU** plan to keep the setup lightweight but efficient.
4. **Configure the Server**:
   - Unselect any default features that aren’t necessary.
   - Assign a hostname, such as **"Ubuntu-SSH-Server"**, to easily identify the machine.
5. **Deploy the VM**:
   - After completing the configuration, click **Deploy Now**. Your VM will be ready in a few minutes.

---

#### Step 2: Reviewing Authentication Logs on the VM

Once the VM is running and you’re connected via **SSH**, it’s time to check the **authentication logs** for any login attempts:

1. **Update and Upgrade the VM**:
   - Run the following command to ensure all packages are up to date:
     ```bash
     sudo apt update && sudo apt upgrade -y
     ```

2. **Navigate to Authentication Logs**:
   - All authentication logs are stored in the **/var/log** directory.
   - Use the following command to navigate there:
     ```bash
     cd /var/log
     ```

3. **View Authentication Logs**:
   - To review the authentication logs, use the `cat` command:
     ```bash
     cat auth.log
     ```
   - This will display the entire authentication log, where you can see both successful and failed login attempts.

4. **Filter Specific Logs**:
   - To focus on logs related to a specific user (e.g., **root**), use the `grep` command to filter the output:
     ```bash
     cat auth.log | grep -i root | cut -d ' ' -f 2
     ```
   - Breakdown of the command:
     - `grep -i root`: Searches for any instance of "root" in a case-insensitive manner.
     - `cut -d ' ' -f 2`: Extracts the second field (timestamp) from the matching lines.

   This command allows you to focus on critical details like login times and any failed attempts related to the root user. 

---

### Summary

On **Day 12**, we successfully deployed an **Ubuntu server** with **SSH** enabled on a cloud platform, gaining hands-on experience with monitoring authentication logs in real-time. You learned how to filter and view logs, including failed login attempts that could indicate potential **brute force attacks** — a topic we discussed in **Day 11**.

Tomorrow, we’ll move on to **installing the Elastic Agent** on your Ubuntu server, allowing us to forward logs directly into **Elasticsearch** for centralized monitoring and analysis.
### Day 13: Install Elastic Agent on Ubuntu Server

Welcome to Day 13 of the 30-Day MYDFIR SOC Analyst Challenge! Today, we’ll be installing the **Elastic Agent** on the **Ubuntu server** that we set up earlier. By connecting it to your **Elasticsearch** instance, you’ll be able to streamline log management and conduct efficient log analysis directly from your Ubuntu machine.

---

#### Step 1: Start Your ELK Server

Before beginning the installation of the Elastic Agent, make sure your **ELK server** is up and running.

- **Run Elasticsearch**: Ensure Elasticsearch is accessible through the web GUI. You’ll need it to interact with the Elastic Agent during the installation process.

---

#### Step 2: Create a New Agent Policy

1. **Access Fleet**:
   - Click on the hamburger menu (three lines) on the left of the ELK dashboard.
   - Scroll down to the **Fleet** section under **Management**.
2. **Create a New Agent Policy**:
   - In Fleet, go to **Agent Policies** and click **Create Agent Policy**.
   - Name your policy according to your preference and click **Create**.
3. **Review the Policy Details**:
   - After creating the policy, click on its name to view its details.
   - In the **Inputs** section, you’ll see the default system input that controls which logs are sent to Elasticsearch.

---

#### Step 3: Customize the Log Path

1. **Set the Log Path**:
   - Since you’re working on an Ubuntu server, set the log path to **/var/log/auth.log**. This ensures that **authentication logs** from the server are ingested into your Elasticsearch instance.
2. **Save the Configuration**:
   - Once you’ve customized the log path, click **Save** to apply the changes.

---

#### Step 4: Add the Elastic Agent

1. **Enroll the Elastic Agent**:
   - Navigate back to the **Agent Policies** section and click on **Agents**.
   - Click **Add agent** to begin the enrollment process.
2. **Select Your Policy**:
   - Choose the agent policy you created earlier.
   - Under "Enroll in Fleet?", select **Enroll in Fleet (recommended)**.
3. **Copy the Command**:
   - You will see a list of commands for various operating systems. Select the tab for **Linux** and copy the commands.

---

#### Step 5: Install the Elastic Agent on Ubuntu

1. **Open Terminal on Ubuntu**:
   - On your **Ubuntu server**, open the terminal.
   - Navigate to your home directory by typing:
     ```bash
     cd ~
     ```
2. **Install the Elastic Agent**:
   - Paste the command you copied from the Fleet GUI into the terminal and press **Enter**.
   - Follow the prompts during installation. When asked, type **Y** and hit **Enter**.

---

#### Step 6: Fix the X509 Certificate Error

If you encounter the following error:  
“**Failed to execute request to fleet server: x509 certificate signed by unknown authority**,” don’t panic. This is a common issue related to certificate validation.

1. **Bypass the Certificate Validation**:
   - Simply add the `--insecure` flag to the end of the command you ran earlier.
2. **Re-run the Command**:
   - Run the modified command again, and this time the Elastic Agent should install successfully.

---

#### Step 7: Confirm Agent Enrollment

1. **Check the Elastic GUI**:
   - Once the Elastic Agent is installed, return to the **Elastic GUI** to confirm that the agent has been successfully enrolled.
2. **Verify Incoming Data**:
   - You should start seeing data from your Ubuntu server being ingested into **Elasticsearch**. You can now query logs directly, enabling real-time monitoring of authentication events.

---

### Summary

On **Day 13**, you successfully installed the **Elastic Agent** on your Ubuntu server and linked it to your **Elasticsearch instance**. With this setup, you can now monitor logs and track authentication activities on your server in real time. This integration makes log analysis more streamlined and efficient.

Tomorrow, we’ll take things a step further by creating alerts for **brute force attacks** and building dashboards to visualize key security events. Stay tuned!

### Day 14: Creating Alerts and Dashboards in Kibana (Part 1)

Welcome to Day 14 of the 30-Day MYDFIR SOC Analyst Challenge! Today, we’ll go through the steps to create an **SSH brute force alert** and build a **dashboard in Kibana** to visualize where these attacks originate. This will give you real-time insights into potential brute force activity targeting your systems, based on the logs ingested from your Ubuntu server.

---

#### Step 1: Query for Failed SSH Authentication Attempts

To begin, we’ll query for logs related to **failed SSH authentication attempts**, which are key indicators of brute force activity.

1. **Add the Relevant Field**:
   - In Kibana, look for the field **system.auth.ssh.event** in the left panel and click the **+** button to add it as a column.
   - Filter for logs where this field exists by clicking the **filter** button, typing **system.auth.ssh.event**, and selecting **exists**.
     ```bash
     system.auth.ssh.event: * and agent.name: <your-linux-agent-name> and system.auth.ssh.event: Failed
     ```

2. **Add More Fields**:
   - Add **user.name** to track the username associated with the login attempt.
   - Add **source.ip** to track the IP address of the failed login attempts.
   - Add **source.geo.country_name** to track the country of origin for these attempts.

3. **Save the Query**:
   - Once you’ve configured your query, click the save icon in the top-right corner.
   - Name it something like **"SSH Failed Activity"** and save it for future use.

---

#### Step 2: Create an Alert for Brute Force Attacks

With your query set up, it’s time to create an alert that will notify you when brute force activity is detected.

1. **Create a Search Threshold Rule**:
   - Click on the **Alerts** tab in the top-right corner, then select **Create search threshold rule**.
   - Give your alert a meaningful name, and Kibana will automatically populate the search query based on your saved query.

2. **Set the Conditions**:
   - Define a threshold, such as **more than 5 failed attempts within 5 minutes**.
   - Set the threshold to **"is above 5"** and adjust the time range to **5 minutes**.

3. **Test and Save**:
   - Test the query using the **Test Query** button and make any necessary adjustments.
   - Save the rule by clicking **Save Rule**. You can add actions later, such as sending notifications when the rule is triggered.

---

#### Step 3: Create a Dashboard to Visualize Brute Force Attempts

Next, we’ll create a dashboard to visualize where these brute force attempts are coming from.

1. **Load the Map Interface**:
   - Go to the hamburger menu in the top-left, click on **Maps** under the **Analytics** tab.
   - Copy the query you previously created (**SSH Failed Activity**) and paste it into the map’s search field.

2. **Add a Layer to Visualize Attacks**:
   - Click **Add Layer**, and choose **Choropleth** to highlight the geographic areas where attacks originate.
   - Use **EMS boundaries** to display country borders on the map.
   - Select your data index and set the join field to **source.geo.country_iso_code** for accurate visualization.

3. **Save and Add to Dashboard**:
   - Save the map with a title like **"SSH Network Map"**.
   - Click **Add to Dashboard** and select **Create New Dashboard** to integrate it into a fresh dashboard.

---

#### Step 4: Customize Your Dashboard

Now that your map is added, let’s customize the dashboard for real-time monitoring.

1. **Rename the Dashboard**:
   - Name the dashboard something like **"Authentication Activity"** to reflect its purpose.

2. **Set the Time Range**:
   - Adjust the time range to your preference, such as the **last 30 days** or **last 1 minute** for real-time monitoring.
   - This ensures you can track current and historical brute force activity effectively.

---
My dashboard is given below and shows SSH Authentication Activities via Geo Locations for both Failed (Left of the dashboard) and Accepted (Right of the dashboard).

![[Screenshot 2024-09-16 at 4.43.47 PM.png]]
### Summary

On **Day 14**, you successfully created an **alert** and a **dashboard** in Kibana to monitor **SSH brute force activity**. The alert notifies you when suspicious login attempts are detected, while the dashboard provides a visual map of where these attacks originate, helping you stay on top of security incidents.

Tomorrow, we’ll explore a commonly exploited service often abused in organizations and how to protect against it. Stay tuned!

### Day 15: Understanding & Securing RDP

Welcome to Day 15 of the 30-Day MYDFIR SOC Analyst Challenge! Today, we’ll focus on **Remote Desktop Protocol (RDP)**, a widely used Microsoft protocol for remote access. While RDP is a valuable tool for remote administration and support, it has become a prime target for attackers. In this post, we'll explore how RDP works, how it's abused, and most importantly, how you can secure your systems against RDP-based attacks.

---

#### What is RDP?

**Remote Desktop Protocol (RDP)** is a protocol developed by Microsoft that enables users to connect remotely to another machine over a network. It allows users to control a machine as though they were physically present, providing essential functionality for remote work, troubleshooting, and administrative tasks.

- **Default Port**: RDP operates on **port 3389** and uses **TCP** for communication.
- **Use Case**: It’s popular for enabling **remote work**, **IT troubleshooting**, and **convenience** by eliminating the need for physical presence.

---

#### Why is RDP Used?

RDP is widely used for various purposes, including:

1. **Remote Work**: Employees can access their workstations from home or other locations.
2. **Troubleshooting**: IT support can diagnose and fix issues on a remote machine without being physically present.
3. **Efficiency**: It saves time and resources by reducing the need for on-site visits, making it ideal for remote administration.

However, despite its utility, RDP is a frequent target of attackers. In fact, **Sofos** reported that **90% of ransomware breaches in 2023** involved RDP abuse.

---

#### How is RDP Abused?

Attackers exploit exposed RDP services to gain unauthorized access to systems and networks. Here's how they typically abuse RDP:

1. **Exposure**: Many RDP services are publicly accessible, often without proper security configurations.
2. **Brute Force Attacks**: Attackers use automated tools to try numerous password combinations until they find valid credentials.
3. **Credential Harvesting**: Once inside, attackers often perform credential dumping to gain more user credentials.
4. **Lateral Movement**: After harvesting credentials, attackers move across the network, gaining access to more systems. This can result in data theft or ransomware deployment.

---

#### How to Find Exposed RDP Servers

Exposed RDP services are a significant security risk, but you can identify them using the following tools:

1. **Shodan**:
   - Visit **Shodan.io** and create an account.
   - Search for **port:3389** to find publicly accessible servers running RDP.
![[Screenshot 2024-09-16 at 4.51.02 PM.png]]
   
2. **Censys**:
   - Go to **Censys.io** and search for **3389**.
   - Filter the results to locate RDP services that are exposed to the internet.

![[Screenshot 2024-09-16 at 4.57.23 PM.png]]

These tools help identify risks so you can take corrective actions. However, **do not attempt to connect or brute-force these servers**—the goal is to assess exposure, not attack.

---

#### How to Protect Yourself from RDP Abuse

Protecting your systems from RDP abuse involves implementing several best practices:

1. **Turn Off RDP When Not Needed**:
   - Disable RDP on development servers or machines where it’s not necessary.
   - Regularly check for exposed RDP services using tools like **Shodan** and **Censys**.

2. **Use Multi-Factor Authentication (MFA)**:
   - Implementing **MFA** adds an extra layer of protection. Even if an attacker guesses the password, they won’t be able to access the machine without the additional authentication factor.

3. **Restrict Access**:
   - Use firewall rules to limit RDP access to specific **IP ranges** or secure it behind a **VPN**.
   - This limits exposure and reduces the chance of unauthorized scanning or brute-force attacks.

4. **Use Strong Passwords**:
   - Ensure passwords are long (at least **15 characters**) and complex, combining upper and lowercase letters, numbers, and special characters.
   - Consider using **Privileged Access Management (PAM)** tools for one-time passwords to further secure access.

5. **Change Default Accounts**:
   - Disable default local accounts and create **unique administrator accounts** with non-standard names.
   - This prevents attacks that rely on common or default credentials.

---

### Summary

On **Day 15**, we explored **Remote Desktop Protocol (RDP)**, its uses, and the risks associated with leaving RDP services exposed. By understanding how attackers exploit RDP through brute force and credential theft, and implementing security measures like **disabling unused RDP services**, **using MFA**, and **restricting access**, you can significantly reduce the risk of unauthorized access and potential breaches.

Tomorrow, we’ll take this a step further by analyzing RDP logs from a **Windows server** and setting up alerts to detect brute-force attempts. Stay tuned!

### Day 16: Creating Alerts & Dashboards in Kibana (Part 2)

Welcome to Day 16 of the 30-Day MYDFIR SOC Analyst Challenge! Today, we’ll build on the previous Kibana work by reviewing **authentication logs** from our Windows server (created on Day 5), setting up detailed **brute-force alerts**, and creating **detection rules** for our Windows and Ubuntu servers. By the end of today, you’ll have alerts monitoring both SSH and RDP brute-force attempts, giving you deeper insights into suspicious activities.

---

#### Step 1: Start the ELK Server and Windows Machine

1. **Start the Machines**: Make sure both your **ELK server** and **Windows machine** are running.
2. **Open Kibana**: Access the **Kibana Web GUI** from your ELK server.
3. **Navigate to Discover**:
   - Click the **hamburger icon** in the top-left and select **Discover**.
   - Filter the logs by selecting the **Windows agent** from the left panel and clicking the **plus** button.

---

#### Step 2: Finding Failed Authentication Logs

1. **Search for Failed Logons**:
   - Failed logon attempts are typically recorded with **Event ID 4625**.
   - In Kibana, search for this event by querying for `event.code:4625`. This will show all failed login attempts.
   
2. **Track Failed Logons**:
   - In the logs, find the fields containing the **event code** (event.code) to help track these failed logins.

---

#### Step 3: Modify the Table to Include Relevant Data

1. **Add Important Fields**:
   - Search for **source.ip** in the left panel and add it as a column.
   - Add **user.name** to track the username associated with the login attempt.
   
2. **Save the Query**:
   - Save this query by clicking the **save button** in the top-right corner.
   - Give it a title like **"RDP Failed Activity"** and save it for future use.
   
3. **Focus on RDP Logs**:
   - RDP and SMB authentications typically use **logon type 3**.
   - For successful logons, use **Event ID 4624**, which tracks various logon types like interactive and network logons.

---

#### Step 4: Create an Alert for Windows Server

1. **Create an Alert**:
   - Go to the **hamburger icon**, scroll down, and select **Create Search Threshold Rule**.
   - Name the alert **RDP Brute Force Activity** and set the query to `event.code:4625`.
   
2. **Configure the Alert**:
   - Set the condition: If there are more than **5 failed attempts within 5 minutes**, trigger an alert.
   - Set the rule to check every **1 minute**.
   
3. **Save the Rule**:
   - Save the alert by clicking the **Save** button.

---

#### Step 5: View Generated Alerts

1. **Check for Alerts**:
   - Go to **Stack Management > Alerts** to see any generated alerts.
   
2. **Simulate Failed Logons**:
   - If no alerts are generated, you can simulate failed logins on your Windows machine to trigger the alert.

3. **Review Alert Details**:
   - When an alert is triggered, click to view its details. Note that basic alerts may not provide information like the source IP or username, so we will improve this in the next step.

---

#### Step 6: Creating a Detailed Rule-Based Alert for Ubuntu Server

1. **Create a Detailed Rule**:
   - Go to **Security > Rules > Detection Rules** and click **New Rule**.
   - Select **Threshold** as the rule type.

2. **Configure the Custom Query**:
   - Use the saved query or copy the query from **SSH alert** tasks (from earlier days).
   - Modify the query to include `user.name:root` for the Ubuntu server, as the root user is unique to the SSH server.
   
3. **Group by User and Source IP**:
   - Group the query by **user.name** and **source.ip** to track failed attempts more effectively.

4. **Set Severity and Name the Rule**:
   - Set the severity to **Medium** and name the rule **SSH Brute Force Attempt**.
   - Add a description, such as "This rule detects failed authentications towards the root user."

5. **Advanced Settings**:
   - You can add **false positive** examples or **MITRE ATT&CK tactics** in production environments, but we’ll leave this blank for now.
   
6. **Create and Enable the Rule**:
   - Set the rule to run every **5 minutes**, with a look-back period of 5 minutes.
   - Click **Create and Enable Rule**.

![[Screenshot 2024-09-16 at 5.02.07 PM.png]]

---

#### Step 7: Create a Detailed Rule-Based Alert for Windows Server

1. **Repeat for RDP Brute-Force Attempts**:
   - Follow the same steps as the Ubuntu alert but modify the query for the **Windows server**.
   - Change the query to `user.name:ADMINISTRATOR`, as this user exists on the Windows machine.

2. **Group by Source IP and User**:
   - Group the results by **source.ip** and **user.name** to track failed RDP logins.

3. **Set the Schedule**:
   - Set the rule to run every **1 minute**, with a look-back time of 5 minutes.

4. **Create and Enable Rule**:
   - Name this rule **RDP Brute Force Attempt** and set the severity to **Medium**.
   - Click **Create and Enable Rule**.
![[Screenshot 2024-09-16 at 5.02.44 PM.png]]

---

#### Step 8: Verify Alerts

1. **View Alert Details**:
   - Go to **Alerts** to verify the details of each triggered alert.
   - Alerts will now contain additional information such as the **source IP**, **username**, and other relevant details.

2. **Note on Visualizations**:
   - Unfortunately, advanced visualizations require an **enterprise subscription**. However, you can still view useful insights like the **server’s SID**, **user ID**, and more.

Overall, based on the alerts created, we got 4 alerts that were raised.

![[Screenshot 2024-09-16 at 5.07.14 PM.png]]

---

### Security Recommendations

- **Understand Exposed Services**: Identify which services like **SSH** or **RDP** are exposed to the internet.
- **Use MFA and Strong Passwords**: Enable **Multi-Factor Authentication** and use strong, unique passwords to protect access.
- **Limit Access**: Restrict access to these services to only authorized users or IP ranges to reduce exposure.

---

### Summary

On **Day 16**, you learned how to review authentication logs from your **Windows server**, create **brute-force alerts** for both SSH and RDP, and set up **detailed rule-based alerts** for better security monitoring. These rules allow you to detect suspicious activity in real-time and provide detailed information on failed login attempts.

Tomorrow, we’ll focus on creating a **dashboard** to visualize these security events, giving you a centralized view of your system’s security posture. Stay tuned!

### Day 17: Creating Alerts & Dashboards in Kibana (Part 3)

Welcome to Day 17 of the 30-Day MYDFIR SOC Analyst Challenge! Today, we’ll complete our **Kibana dashboard** by focusing on **Remote Desktop Protocol (RDP) activity**, specifically tracking both failed and successful authentication attempts on a **Windows server**. Using the data generated from our Windows agent, we’ll create visual maps and data tables for a detailed overview of RDP activity. Let’s dive in!

---
#### Step 1: Setting Up the Environment

1. **Open Kibana**: Ensure your **Elastic web GUI** is running and your **Windows agent** is set up.
2. **Navigate to Maps**: Click the **hamburger icon** on the left-hand side of the Elastic web GUI and select **Maps**. This is where we’ll build our visualizations.

---
#### Step 2: Generating the Query

1. **Open Discover**:
   - Go to the **Discover tab** in Kibana to retrieve data related to authentication attempts.
   - Set the **time filter** to cover the last **7 days** to ensure you capture enough relevant data.

2. **Modify the SSH Query for RDP**:
   - Copy your saved **SSH activity query** and paste it into a notepad. This is the query for RDP failed logins.
   - Modify the query to focus on RDP by adding:
     ```bash
     event.code: 4625 and agent.name: <your-windows-agent-name>
     ```

3. **Apply the Query in Maps**:
   - Go to the **Maps tab**, paste the modified query into the search box, and click **Update**.

---

#### Step 3: Creating the Map Layer for Failed RDP Authentications

1. **Add a Layer**:
   - In Maps, click **Add Layer** and choose **Choropleth** for a visual map layer.
   
2. **Set Layer Options**:
   - **EMS Boundary**: Select **World Countries**.
   - **Data View**: Choose the appropriate data view for alerts, such as `.alerts`.
   - **Join Field**: Set it to **source.geo.country_iso_code** to visualize where the attacks are originating.

3. **Save the Map**:
   - Name the map something like **"RDP Failed Authentication"** and add it to the SSH dashboard you created previously.

---

#### Step 4: Adding a Map for Successful RDP Authentications

1. **Identify Event ID for Successful Logons**:
   - Successful RDP logons are associated with **Event ID 4624**, specifically **Logon Types 7 and 10**.

2. **Modify the Query**:
   - Update your saved query in the notepad to track successful logons:
     ```bash
     event_id: 4624 and (winlog.event_data.LogonType: 7 or winlog.event_data.LogonType: 10)
     ```

3. **Duplicate the Map**:
   - Go back to **Maps**, duplicate the map you created for **RDP failed authentications**, and replace the query with the new query for successful RDP authentications.

4. **Save and Add**:
   - Save the duplicate map as **"RDP Successful Authentication"** and add it to your dashboard.

---

#### Step 5: Enhancing the Dashboard with Data Tables

1. **Create a Table for Failed RDP Activity**:
   - Go back to the **hamburger icon**, click **Failed RDP Activity**.
   - Add the following columns to the table: **Time**, **Source IP**, **Username**, and **Country**.

2. **Organize the Table**:
   - Arrange the columns as needed (e.g., **Timestamp** on the left, followed by **Username**, **Source IP**, and **Country**).
   
3. **Save the Table**:
   - Add the table to the **Maps dashboard** and save your progress.

---

#### Step 6: Creating a Table for Successful RDP Authentications

1. **Duplicate the Failed RDP Table**:
   - Duplicate the table created for **failed RDP authentications**.
   
2. **Replace the Query**:
   - Replace the query with the one you created for **successful RDP logons**.
   
3. **Save the Table**:
   - Save the table as **"Successful RDP Authentication"** and add it to your dashboard.

---

#### Step 7: Adjusting Table Settings

1. **Increase Top Values**:
   - For both tables (failed and successful), increase the **Top 3 values to 10** for **usernames** and **source IPs**.

2. **Disable Grouping**:
   - In **Advanced Settings**, disable the **Group Remaining as Other** option to prevent lesser values from being grouped.

3. **Sort by Frequency**:
   - Sort the tables in **descending order** so the most frequent failed or successful logins appear at the top.

---

#### Step 8: Adding SSH Data to the Dashboard

1. **Duplicate RDP Tables for SSH**:
   - Duplicate the tables for RDP failed authentications and successful logons.
   - Replace the queries with those used for SSH activity.

2. **Add to Dashboard**:
   - Add these tables to the dashboard so you have a unified view of both **RDP** and **SSH** activity.

---

#### Step 9: Saving the Dashboard

1. **Save Your Progress**:
   - Don’t forget to save your work by clicking the **Save** button in the Maps tab.
   
2. **Final Overview**:
   - Your dashboard should now include:
   
- **Maps** for both **failed and successful SSH & RDP authentications**.

![[Screenshot 2024-09-17 at 2.05.23 PM.png]]

- **Tables** for both **failed and successful SSH authentications**.

![[Screenshot 2024-09-17 at 2.04.42 PM.png]]

---

### Summary

On **Day 17**, you created a comprehensive **Kibana dashboard** that tracks **RDP** and **SSH authentication attempts** on your Windows server. This dashboard provides both **visual maps** and **detailed tables**, giving you an at-a-glance view of both failed and successful logon attempts. This setup is essential for monitoring and detecting potential brute force attacks and unauthorized access.

In tomorrow’s session, we’ll explore **Command and Control (C2) tactics** and introduce the **Mythic framework**, used by attackers to establish C2 sessions. Stay tuned!

### Day 18: Introduction to Command and Control (C2)

Welcome to Day 18 of the 30-Day MYDFIR SOC Analyst Challenge! Today, we’re exploring a crucial aspect of cyberattacks known as **Command and Control (C2)**. Once attackers gain access to a system, they typically perform initial tasks like gathering system details (e.g., using commands like `ipconfig` or `whoami`) and establishing persistence. However, the most important step that follows is setting up a **C2 session**, which allows attackers to remotely control the compromised system.

In this post, we’ll explore what C2 is, why it’s essential to an attacker’s operation, and some common tools used to establish C2 channels. By the end of this, you’ll have a solid understanding of how C2 sessions fit into the broader scope of a cyberattack. Let’s jump in!

---

### What is Command and Control (C2)?

**Command and Control (C2)** refers to the methods attackers use to communicate with and control systems they’ve successfully compromised. Using frameworks like **MITRE ATT&CK**, C2 involves techniques that enable attackers to remotely direct actions on infected machines within the victim’s network. Once C2 is established, the attacker can issue commands, steal data, move laterally across the network, or deploy additional payloads.

Essentially, C2 is the attacker’s remote interface into the compromised environment, allowing them to persist and execute their mission, whether that’s data exfiltration, credential theft, or delivering ransomware.

---

### Why is C2 Important?

C2 is vital because it allows attackers to maintain access to a system after the initial compromise. With C2, they can:

- **Move laterally**: Attackers can jump between systems within a network.
- **Harvest credentials**: Attackers can gather login information to escalate privileges.
- **Exfiltrate data**: Sensitive information can be stolen and sent to an external server.
- **Deploy malware**: Additional payloads, like ransomware or spyware, can be deployed.

Without a reliable C2 channel, attackers would lose their ability to maintain control over a system after the initial breach. MITRE ATT&CK outlines 18 techniques that adversaries can use to establish C2 communications, highlighting the importance and versatility of C2 in the attack lifecycle.

---

### Common Tools and Frameworks for C2

Attackers have developed numerous tools and frameworks to establish C2 sessions, many of which are also used by penetration testers and red teams for adversary emulation. Let’s explore some of the most well-known:

1. **Metasploit**
   - A popular tool for penetration testers, Metasploit provides an extensive collection of exploits and auxiliary modules. It’s often used to identify and exploit vulnerabilities, giving attackers a way to gain a foothold and set up C2.

2. **Cobalt Strike**
   - Although a legitimate adversary simulation tool for red teams, Cobalt Strike is frequently used in real-world attacks. Its flexibility and extensive feature set make it a favorite for establishing C2 channels. Detection tools have become more adept at spotting Cobalt Strike due to its widespread use in cyberattacks.

3. **Sliver**
   - An open-source alternative to Cobalt Strike, **Sliver** is gaining popularity in the attacker community. It supports various communication protocols, including HTTP/HTTPS, DNS, and WireGuard, making it versatile for establishing C2 connections.

4. **Mythic**
   - **Mythic** is a modern C2 framework designed for flexibility and ease of use. Built with Go, Docker, and a web-based interface, it supports multiple agents and C2 profiles, making it a powerful tool for managing and tracking compromised machines. It’s often favored for its modularity and the ability to customize payloads and communication methods.

---

### Summary

**Command and Control (C2)** is a pivotal part of a cyberattack, allowing attackers to remotely manage compromised systems, steal data, escalate privileges, and deploy additional malicious software. Today, we’ve explored what C2 is, why it’s essential to an attacker’s success, and some of the popular tools used to establish C2 connections, including **Metasploit**, **Cobalt Strike**, **Sliver**, and **Mythic**.

Tomorrow, we’ll take this knowledge further by setting up our own **Mythic C2 server**, crafting an agent, and establishing a C2 session on a Windows server. Stay tuned!

### Day 19: Designing an Attack Diagram

Welcome to Day 19 of the 30-Day MYDFIR SOC Analyst Challenge! Today, we’re focusing on a key aspect for any **SOC Analyst**: crafting an **Attack Diagram**. This visual map will help us outline every stage of a cyberattack — from the initial compromise to establishing Command and Control (C2) and, ultimately, exfiltrating data. By the end of today’s task, you’ll have a strong visual representation of an attack flow, which is vital for both understanding and responding to incidents.

---

### Why Create an Attack Diagram?

Creating an **Attack Diagram** is more than just an exercise in visualization; it’s a tool that helps you:

- **Understand the attack**: Each phase of the attack becomes clearer, making it easier to anticipate the attacker’s next move.
- **Plan countermeasures**: Knowing the attack flow helps defenders identify weak points and deploy appropriate defenses.
- **Prepare for post-compromise analysis**: It becomes easier to analyze what went wrong and how to prevent future breaches.

Now, let’s dive into the steps to create our diagram.

---

### Building the Attack Diagram

We’ll use **draw.io** (what we used in Day 1 to build out our Logical Diagram), a simple but effective diagramming tool, to visually map out the phases of the attack. The diagram will track each major step, from gaining access to exfiltrating data. Here are the core components and phases of the attack.

---

#### Core Components

1. **Attacker’s Computer**: A **Kali Linux** machine used to perform reconnaissance and launch the brute-force attack.
2. **Mythic C2 Server**: The command center for managing post-compromise activities, hosted on a cloud platform like AWS.
3. **Windows Server**: The main target of the attack, where we’ll use RDP brute-force techniques to gain access.
4. **Optional SSH Server**: A secondary target for those interested in practicing additional attack vectors.

---

### Phases of the Attack

#### Phase 1: Initial Access — Brute Force Attack on RDP

In the first phase, the goal is to break into the **Windows Server** using a **brute-force attack** on **Remote Desktop Protocol (RDP)**.

- **Action**: Launch a brute-force attack from **Kali Linux**, targeting the Windows Server’s RDP.
- **Outcome**: Successfully gain a valid session on the Windows machine after multiple login attempts.

![[Screenshot 2024-09-19 at 2.03.38 PM.png]]

---

#### Phase 2: Discovery

Now that we’ve gained access, it’s time to gather information about the compromised system. This phase is all about running **discovery commands** to understand the system’s layout, network connections, and user privileges.

- **Action**: Use the RDP session to run commands like `whoami`, `ipconfig`, and `net user`.
- **Outcome**: Collect key information on the system’s configuration, network setup, and available user privileges.

![[Screenshot 2024-09-19 at 2.04.03 PM.png]]

---

#### Phase 3: Defense Evasion

To move further into the network undetected, we need to disable security mechanisms. In this case, we’ll focus on **disabling Windows Defender**, reducing the system’s defenses.

- **Action**: Attempt to disable **Windows Defender** via the RDP session.
- **Outcome**: Weaken the system’s defenses, making it more vulnerable to subsequent attacks.

![[Screenshot 2024-09-19 at 2.04.16 PM.png]]

---

#### Phase 4: Execution — Deploying the Mythic Agent

With defenses lowered, we can deploy our attack payload — the **Mythic Agent**. This agent will be downloaded and executed using **PowerShell**, allowing us to gain full control of the compromised machine.

- **Action**: Use **PowerShell’s Invoke-Expression (IEX)** command to download and execute the Mythic Agent from the Mythic C2 server.
- **Outcome**: Successfully deploy the payload, granting control over the Windows machine.
![[Screenshot 2024-09-19 at 2.04.35 PM.png]]

---

#### Phase 5: Command and Control (C2)

With the **Mythic Agent** active, we now establish a C2 session. This is where we take remote control of the compromised machine, issuing commands and manipulating it from our Mythic C2 server.

- **Action**: Verify the establishment of the **C2 session** and begin issuing remote commands.
- **Outcome**: Gain full control over the Windows server, with the ability to execute commands remotely.
![[Screenshot 2024-09-19 at 2.04.51 PM.png]]

---

#### Phase 6: Exfilration

To simulate a real-world attack, we’ll create and steal a sensitive file. In this phase, we generate a dummy file (`passwords.txt`) and use our C2 session to exfiltrate it, demonstrating how attackers steal data.

- **Action**: Create a fake file (`passwords.txt`) on the compromised machine and use the **C2 channel** to transfer it.
- **Outcome**: Successfully simulate a data breach by exfiltrating sensitive data.

![[Screenshot 2024-09-19 at 2.05.06 PM.png]]
---

### Summary

By following these six phases, you’ve mapped out a complete **Attack Diagram** that outlines each step — from the initial compromise via brute-force RDP attacks to establishing a **C2 session** and exfiltrating data. This visual representation is an excellent resource for understanding the flow of an attack and for planning defense strategies.

In tomorrow’s task, we’ll set up our **Mythic C2 server** and walk through the key steps of configuring it. We’ll also explore how the **Mythic framework** operates as a tool for managing post-compromise activities. Stay tuned!

### Day 20: Mythic C2 Server Installation (Part 1)

Welcome to Day 20 of the 30-Day MYDFIR SOC Analyst Challenge! Today, we will  explored how to set up a **Mythic C2 instance** and gain a solid understanding of its configuration and functionality. **Mythic** is a powerful tool for command and control (C2) operations, and today’s task focused on getting it up and running on an Ubuntu server. Let’s go through the steps I followed to set everything up.

---

### Step 1: Set Up a Vultr Server

First, I needed to deploy a new server on **Vultr**:

1. Go to Vultr and choose **Cloud Compute — Shared CPU**.
2. Select the same location as your **VPC 2.0**.
3. Pick **Ubuntu 22.04 LTS** as the operating system.
4. Opt for the **50GB NVMe, 1 CPU, and 2GB RAM** plan.
5. Keep all additional features unchecked.
6. Set the server’s hostname and label according to your preferences.
7. Click **Deploy Now** and wait for your server to be ready.

---

### Step 2: Download Kali Linux

To complement the attack, I also set up **Kali Linux**:

1. Head over to the **Kali Linux website** and download the **Virtual Machine (VM)** version for your preferred hypervisor (e.g., VMware).
2. Once downloaded, unzip the file, find the **.vmx** file, and double-click it to import Kali into **VMware Workstation**.
3. Power on Kali Linux, and it’s ready to go!

---

### Step 3: SSH into Your Server

Now it’s time to log into the **Ubuntu server**:

1. Open **Vultr**, and from the console, copy your server’s **public IP address**.
2. Open **PowerShell** or your terminal and type:
   ```bash
   ssh root@<public-ip-of-machine>
   ```
3. When prompted, press **Y**, and enter the password provided by Vultr.
4. You’re now logged into your Ubuntu server!

---

### Step 4: Update and Install Prerequisites

To prepare the server, I updated the system and installed the required tools:

1. Update and upgrade your repositories:
   ```bash
   apt update && apt upgrade
   ```
2. Install **Docker Compose**:
   ```bash
   apt install docker-compose
   ```
3. Install **make**:
   ```bash
   apt install make
   ```

---

### Step 5: Clone the Mythic Repository

Now it’s time to install **Mythic**:

1. Clone the Mythic repository:
   ```bash
   git clone https://github.com/its-a-feature/Mythic
   ```
2. Navigate into the **mythic** directory:
   ```bash
   cd mythic
   ```
3. Install Docker and Mythic using the provided script:
   ```bash
   ./install_docker_ubuntu.sh
   ```

---

### Step 6: Start Mythic

Once Mythic is installed, it’s time to start the server:

1. Run the Mythic service with:
   ```bash
   make
   ```
2. If Docker isn’t running, check the status:
   ```bash
   systemctl status docker
   ```
   - If Docker has failed, restart it with:
     ```bash
     systemctl restart docker
     ```

3. Once Docker is running, restart Mythic:
   ```bash
   ./mythic-cli start
   ```

---

### Step 7: Configure Firewall

To secure your environment, I set up firewall rules:

1. In **Vultr**, go to **Firewall** settings.
2. Create a new firewall group, and set the **protocol** to **TCP**.
3. Define the port range as **1–65535**, and set the source to your **IP address**.
4. Add additional rules for your **Windows machine** and **Ubuntu server**.
5. Apply this firewall group to your **Ubuntu server** to ensure security.

---

### Step 8: Log in to the Mythic GUI

Now that Mythic is running, it’s time to access the **Mythic GUI**:

1. In your browser, go to:
   ```bash
   https://<public-ip-of-your-server>:7443
   ```
2. Use **mythic_admin** as the username.
3. To get the password, navigate to the **.env** file in the Mythic directory:
   ```bash
   cat .env
   ```
4. Copy the **MYTHIC_ADMIN_PASSWORD** and use it to log in.
5. The Mythic GUI will open, and you’ll be greeted by the dashboard, although there won’t be any agents or callbacks at this point.

![[Screenshot 2024-09-20 at 11.25.30 AM.png]]

![[Screenshot 2024-09-20 at 11.26.43 AM.png]]
---

### Key Features of the Mythic GUI

- **Dashboard Overview**: A snapshot of the environment, showing system health, active agents, and recent activity.
- **Agent Management**: View and manage agents that represent the compromised systems.
- **Callbacks**: Track incoming callbacks from deployed agents and monitor command responses.
- **Commands**: Issue pre-defined or custom commands to the agents.
- **Settings**: Configure user management, permissions, and environment variables.
- **Logs**: View detailed logs to analyze agent activity and performance.

---

### Summary

Setting up the **Mythic C2 server** is an essential step in understanding command and control operations. Mythic is a powerful framework that, when used correctly, can manage agents, issue commands, and track activities in a secure and controlled environment.

In tomorrow’s session, we’ll take this one step further by **creating our own Mythic agent** and launching it on the **Windows server** we set up earlier, simulating a real-world attack scenario. Stay tuned!

### Day 21: Mythic C2 Server Installation (Part 2)

Welcome to Day 21 of the 30-Day MYDFIR SOC Analyst Challenge! Today’s session will take us through an exciting journey of crafting an attack from start to finish using Mythic C2 and various penetration testing tools. This task involved setting up a password file, performing a brute-force attack, and leveraging Mythic to establish control over the Windows server. Each phase deepened my understanding of key penetration testing techniques and the power of Mythic.

---

### Phase 1: Setting Up the Environment

1. **Access the Windows Server** via the Vultr console and log in with Ctrl + Alt + Delete.
2. Navigate to the **Documents folder** and create a new text file named **passwords.txt**.
3. Add the password **Winter2024!** to simulate a realistic scenario.
4. **Change the account password** to **Winter2024!** using the Windows Settings. If any policy errors occur, modify the password policy in **Edit Group Policy** by adjusting the minimum length and disabling the complexity requirements.

---

### Phase 2: RDP Brute Force Attack

1. On **Kali Linux**, prepare a **wordlist** for the attack using the default **rockyou.txt**:
   ```bash
   sudo gunzip /usr/share/wordlists/rockyou.txt.gz
   head -n 50 /usr/share/wordlists/rockyou.txt > ~/mydfir_wordlist.txt
   ```
2. Add the known password **Winter2024!** to the wordlist:
   ```bash
   nano ~/mydfir_wordlist.txt
   ```
3. Install **Crowbar**, an SSH/RDP brute-force tool:
   ```bash
   sudo apt-get update && sudo apt-get install crowbar
   ```
4. Use **Crowbar** to brute-force the RDP login with the following command:
   ```bash
   crowbar -b rdp -u administrator -C ~/mydfir_wordlist.txt -s <Your Windows Server IP Address>/32
   ```
   Once Crowbar finds the correct password, it will display a success message.

---

### Phase 3: Accessing the Windows Server

1. With the correct password, use the following command to access the Windows server via RDP:
   ```bash
   xfreerdp /u:administrator /p:Winter2024! /v:149.248.59.41:3389 /f
   ```
   Approve the certificate prompt and connect to the server.

---

### Phase 4: Running Discovery Commands

Once inside the server, use the **Command Prompt** to run discovery commands:

- `whoami` - Displays the current user (should return **administrator**).
- `ipconfig` - Shows network information.
- `net user` - Lists user accounts.
- `net group` - Shows group memberships (if on a domain controller).

---

### Phase 5: Defense Evasion (Disabling Windows Defender)

To evade detection:

1. Open **Windows Security** and navigate to **Virus & Threat Protection**.
2. Disable **Real-time protection** and other defense mechanisms.

---

### Phase 6: Generating the Mythic Agent

1. **SSH** into your Mythic server.
2. Enter the Mythic CLI environment:
   ```bash
   cd ~/Mythic && ./mythic-cli
   ```
3. As we are focussing on HTTP/TCP mode of Data Exfiltration. We need an appropriate Mythic Agent that helps to achieve this. In this case, we will be using Apollo. Mythic has various other agents with other capabilities that you can check out [here](https://mythicmeta.github.io/overview/agent_matrix.html). For now, install the **Apollo agent**:
   ```bash
   mythic-cli install github.com/MythicAgents/Apollo
   mythic-cli install github.com/MythicProfiles/HTTP
   ```
4. Generate a **Windows executable payload** using Apollo:
   - Go to the Payload tab, choose **Windows** as the platform, and select **Apollo**.
   - Generate the payload with all available commands. I have named the payload "***svchost-aakashraman.exe***".
   
![[Screenshot 2024-09-21 at 12.45.30 PM 2.png]]

![[Screenshot 2024-09-21 at 12.49.01 PM.png]]

![[Screenshot 2024-09-21 at 12.53.04 PM.png]]
5. Use **PowerShell** on the Windows server to download and run the payload, establishing a **C2 session**.

---

### Phase 7: Post-Exploitation

With the C2 session active, use Mythic to retrieve the **passwords.txt** file from the Windows server’s Documents folder. I have used the "download FilePath" command here. You can see all of Apollo's available commands [here](https://github.com/MythicAgents/Apollo).

![[Screenshot 2024-09-21 at 1.26.17 PM.png]]

---

### Summary

Today’s challenge helped me combine several key techniques, including **brute-forcing RDP with Crowbar**, establishing a **C2 session using Mythic**, and running **post-exploitation actions** like file retrieval. Mythic is a highly capable C2 framework, and with practice, it becomes an incredibly powerful tool in penetration testing.

For tomorrow’s task, I’ll be creating **alerts and dashboards** to detect Mythic activities, blending offensive and defensive techniques for better insights into attack detection and response. Stay tuned!

### Day 22: Creating Alerts & Dashboards in Kibana (Part 4)

Welcome to Day 22 of the 30-Day MYDFIR SOC Analyst Challenge! Today’s task focuses on setting up alerts and creating a dashboard in Kibana to detect the Mythic activity that was generated during the attack on **Day 21**. By the end of this guide, you’ll have a solid monitoring system in place to track any suspicious actions related to Mythic agents on your network. Let’s get started!

---

### Step 1: Log in to Your Elastic Web GUI

1. Open the **Elastic Web GUI**.
2. Click the **Hamburger Menu** in the top-left corner.
3. Select **Discover** to begin searching for Mythic activity.

---

### Step 2: Query for Mythic C2 Activity

1. In **Discover**, click **New** to reset everything.
2. Search for the binary you generated earlier, such as `servicehost-aakashraman.exe`. This will help identify Mythic activity.
3. Set the time range to **30 days** to capture all relevant events.
4. Sort the events from **oldest to newest** to see the sequence of actions related to the binary.

---

### Step 3: Analyze the Events

1. Look for events related to `servicehost-aakashraman.exe`. These should be among the first few process creation events.
2. Expand an event and review its details:
   - **Target file name**: Check if the file was placed in `C:\Users\Public\Downloads`.
   - **Username**: Verify if it’s **Administrator**.
   - **Image**: Determine if the process was initiated by **PowerShell**.
   - **Process GUID**: Note this for event correlation later.

---

### Step 4: Filter for Process Creation Events (Event Code 1)

1. Update your query to search specifically for **Process Creation events** (Event Code 1), which offer detailed insight into how Mythic operates:
   ```bash
   event.code: 1 
   ```
2. Look for relevant events that include:
   - **SHA1, MD5, and SHA256 hashes**.
   - **Original file name** (e.g., `apollo.exe`).
3. Take note of the **SHA256 hash** and **original file name** to use in your alert.

---

### Step 5: Check the Hash with VirusTotal

1. Copy the **SHA1 hash** from one of the events.
2. Head to **VirusTotal** and search for the hash to see if any results show up. You might not find any hits since this is a newly generated file, but it’s always good practice to check for known malicious signatures.

---

### Step 6: Create an Alert for Mythic Activity

1. Set up an alert to detect this kind of activity by focusing on:
   - The **SHA256 hash**.
   - The **original file name** (`apollo.exe`).
2. Structure your query using proper conditions and parentheses so that only **Process Creation events (Event Code 1)** trigger the alert:
   ```bash
   event.code: 1 and (winlog.event_data.OriginialFileName: "apollo.exe" or winlog.event_data.Hashes: "your_sha256_hash")
   ```

---

### Step 7: Build the Detection Rule

1. Save your query and name it something like **Mythic Apollo Process Create**.
2. Head to **Detection Rules** in the Elastic GUI and click **Create New Rule**.
3. Use the saved query from Step 6 as the rule’s base.
4. Configure the rule:
   - Set **index patterns** as-is.
   - For the **custom query**, paste the query from Step 6.
5. Define key fields to track:
   - **Username**.
   - **Process GUID**.
   - **Command line**.
   - **Image (process name)**.
6. Set the rule’s severity to **critical** and schedule it to run every **5 minutes**.

---

### Step 8: Create the Dashboard

Now that the alert is set up, we’ll create a dashboard to visualize the activity:

1. Query for **Event ID 3**, which logs network connections:
   ```bash
   event.code: 3
   ```
   Filter for processes initiated by Sysmon and track connections initiated by Mythic agents.
2. Use the **Windlog.event_data.originalFileName** field to identify processes responsible for these external connections.
3. Query for **Event ID 1** to track process creation events related to tools like **PowerShell, CMD**, or **rundll32.exe**.
4. Track **Windows Defender disabling events** by querying for **Event ID 5001**.
5. Add these queries to your dashboard to visualize the full spectrum of Mythic activity.

The final queries would be:

Process Creates - powershell, cmd, rundll32:
```bash
event.code : 1 and event.provider: Microsoft-Windows-Sysmon and (powershell or cmd or rundll32)
```

Network Connections [External] any process initiating a network connection outbound:
```bash
event.code: 3 and event.provider: Microsoft-Windows-Sysmon and winlog.event_data.Initiated: true
	```

Defender Disabled:
```bash
event.code : 5001 and event.provider: Microsoft-Windows-Windows Defender
```


---

### Step 9: Finalize and Review

1. Once you’ve added the panels for **Event ID 1**, **Event ID 3**, and **Event ID 5001**, your dashboard will display a complete view of any suspicious activities.
2. Regularly monitor both the **alerts** and the **dashboard** for potential threats.

![[Screenshot 2024-09-22 at 5.56.11 PM.png]]

![[Screenshot 2024-09-22 at 5.56.21 PM.png]]

![[Screenshot 2024-09-22 at 5.56.28 PM.png]]

---

### Summary

Today, we successfully created a detection rule and built a Kibana dashboard to monitor Mythic C2 activity on your system. By using **process creation events**, **network connection logs**, and tracking changes to **Windows Defender**, you can now effectively identify and respond to malicious activities.

Tomorrow, we’ll delve into building a ticketing systems to prioritise any alerts that come into our ELK SIEM. Stay tuned!

### Day 23: Introduction to Ticketing Systems 

Welcome to Day 23 of the 30-Day MYDFIR SOC Analyst Challenge! Today’s focus is on understanding **ticketing systems** and how they can be leveraged in cybersecurity operations. Ticketing systems are essential for tracking alerts, incidents, and tasks within any organization, especially within a Security Operations Center (SOC). By the end of this introduction, you’ll have a solid grasp of how ticketing systems work and how you can implement one on your own using **osTicket**. Let’s dive in!

---

### What is a Ticketing System?

A **ticketing system** is a tool that helps manage tasks, incidents, and requests by creating digital "tickets." These tickets can represent anything from security alerts to troubleshooting requests or even customer service inquiries. The main function of a ticketing system is to ensure that each task or incident is tracked, addressed, and resolved efficiently. It also provides an **audit trail** for accountability, which is crucial in cybersecurity operations.

In the context of a SOC, ticketing systems help track security alerts, ensuring no potential threat goes unnoticed. Whether it's a misconfiguration or a security incident, a ticketing system helps teams track and respond to alerts systematically.

---

### Why Are Ticketing Systems Important in a SOC?

In a SOC environment, ticketing systems play a vital role in managing and tracking security events. Here’s why they’re essential:

1. **Tracking Incidents**: Every security alert needs to be tracked from detection to resolution. Ticketing systems ensure that no alerts are missed, and they provide a log of every action taken.
2. **Collaboration**: Tickets allow multiple team members to collaborate on a security event, ensuring the right experts are involved in solving complex issues.
3. **Accountability**: Each ticket is assigned to a specific person, ensuring accountability for its resolution.
4. **Auditing**: In the event of an investigation or audit, ticketing systems provide a clear record of all incidents and how they were handled.
5. **Prioritization**: Tickets can be prioritized based on severity, ensuring that critical issues are handled first.

---

### Introducing osTicket

**osTicket** is a free, open-source ticketing system developed by **Enhancesoft**. It provides many of the same features you’d expect in commercial ticketing solutions like **ServiceNow** or **Jira** but at no cost, making it ideal for small businesses, SOCs, or anyone looking to manage alerts efficiently.

Some of osTicket's features include:
- **Customizable ticket fields**: Adapt ticket fields to suit your specific needs.
- **Ticket filters**: Automatically route tickets based on predefined criteria.
- **Assign and transfer tickets**: Easily assign tickets to team members or transfer them across departments.
- **SLAs**: Set up **Service Level Agreements** to ensure tickets are resolved in a timely manner.

osTicket integrates seamlessly with email systems, allowing alerts and incidents to be automatically logged as tickets. This makes it an excellent tool for tracking alerts generated by your security tools.

---

### Why osTicket?

There are several reasons why osTicket is a great choice for SOC environments:

1. **Cost-Effective**: Since osTicket is open-source, it’s free to use, making it ideal for individuals or organizations on a budget.
2. **Customizable**: It can be easily tailored to fit your specific needs, such as adding custom ticket fields or integrating it with your existing security tools.
3. **Hands-On Experience**: Using osTicket gives you valuable experience with ticket management, an essential skill for SOC analysts.
4. **Scalable**: It can be scaled to fit the needs of both small and large teams, making it a flexible solution for growing environments.

---

### How Does a Ticketing System Enhance Security?

By using a ticketing system like osTicket in your SOC operations, you can:

- **Monitor and track** security alerts generated by various tools, ensuring all incidents are logged.
- Ensure **accountability** and **traceability** by assigning incidents to specific individuals or teams.
- Implement **prioritization** and **escalation** policies, ensuring critical alerts are handled promptly.
- Maintain an **audit trail** for future reference or investigations, allowing you to demonstrate compliance and best practices.

---

### Summary

Now that you understand the basics of ticketing systems and how osTicket can be an essential tool for SOC operations, you’re ready to take the next step: **setting up osTicket**. Tomorrow, we’ll cover the step-by-step process to install and configure osTicket, enabling you to start tracking alerts like a SOC professional.

Stay tuned, and get ready to add another powerful tool to your cybersecurity arsenal!

### Day 24: osTicket Setup Tutorial

Welcome to Day 24 of the 30-Day MYDFIR SOC Analyst Challenge! Today, we’ll walk through setting up **osTicket**, a widely-used open-source ticketing system, on a server using **Vultr**, **XAMPP** for Apache and MySQL, and completing the installation of osTicket itself. Follow these steps carefully to get everything set up and running smoothly.

---

### Step 1: Deploying the Server on Vultr

1. **Log into Vultr**: Navigate to your Vultr account and click on **Deploy Instance**.
2. **Select Cloud Compute**: Choose a shared CPU instance for cost efficiency.
3. **Operating System**: Choose **Windows Server 2022 Standard** as your OS.
4. **Server Plan**: Opt for a plan with **1 CPU and 2GB RAM** for smooth operation.
5. **Networking**: Skip IPv6 and auto-backup for now but enable **Virtual Private Cloud** (VPC) for secure networking.
6. **Deploy the Server**: Click **Deploy Now** and wait for the server to be ready (this typically takes around 6 minutes).

---

### Step 2: Remote Access

1. **RDP Login**: Use **Remote Desktop Protocol (RDP)** to access the server with the admin credentials provided by Vultr.
2. **Configure Firewall**: Add firewall settings in Vultr to ensure only trusted IPs (e.g., your SOC laptop) have access to the server.
   - Allow traffic only from your specific IP for increased security.
   - Open ports for **RDP** (3389), **HTTP** (80), and **HTTPS** (443) as needed.

---

### Step 3: Setting Up XAMPP for Apache and MySQL

1. **Download XAMPP**: Head over to **Apache Friends** and download **XAMPP** (you’re using version 8.2.2).
2. **Install XAMPP**: During installation, leave the settings at default, and install it on the **C: drive**.
3. **Open XAMPP Control Panel**: Once installed, open the XAMPP control panel and start both the **Apache** and **MySQL** services.

![[Screenshot 2024-09-24 at 11.49.44 AM.png]]

---

### Step 4: Configuring Apache and phpMyAdmin

1. **Configure Apache**:
   - Open the **Apache configuration file** (httpd.conf) and update the domain name with your server’s **public IP**.
   - This ensures your server is accessible via the public IP.
   
2. **Set Up phpMyAdmin**:
   - Navigate to the **phpMyAdmin** config file (`config.inc.php`), and initially set it to bind to **localhost**.
   - Later, update it to bind to your public IP for external access.
   
3. **Update MySQL Permissions**:
   - Update the MySQL **root user’s permissions** to allow connections from your machine's IP address.
   - Make sure to set a **secure password** for the root account to prevent unauthorized access.

4. **Create Firewall Rules**:
   - Set firewall rules in **Vultr** to allow inbound traffic on **port 80 (HTTP)** and **port 443 (HTTPS)**.
   
---

### Step 5: Installing osTicket

1. **Download osTicket**: Go to the official osTicket site and download the latest version (e.g., **1.18.1**).
2. **Extract Files**: Extract the osTicket archive and move the necessary files to the **htdocs** folder of XAMPP under a directory called **osTicket**.
3. **Rename Configuration File**:
   - Rename the `sl-sample.config.php` file to `os-config.php` to prep for setup.
4. **Access osTicket Setup**:
   - Open a browser and go to **http://your-public-ip/osTicket/upload** to start the installation wizard.

---

### Step 6: Final Configuration

1. **osTicket Setup**:
   - Fill out the osTicket setup form, including:
     - **Helpdesk Name**
     - **Admin Credentials**
     - **Database Information**
   
2. **Manually Create a Database**:
   - Before proceeding with the installation, open **phpMyAdmin** and manually create a database for osTicket.
   - Make sure the **root user** has full privileges over the database.

3. **Complete Installation**:
   - Once the database is created, retry the installation, and osTicket should now successfully set up.

![[Screenshot 2024-09-24 at 12.53.16 PM.png]]

---

### Step 7: Troubleshooting Common Errors

- **Database Errors**: If the database isn’t created during the installation, ensure that you manually create it before running the installer.
- **Access Issues**: If you encounter access issues, verify the firewall settings and **MySQL** user permissions to ensure the correct access is granted.

---

### Summary

You’ve now successfully set up **osTicket** on your server, complete with **XAMPP** and proper firewall settings to ensure a secure and functional helpdesk system. This ticketing system will allow you to track and manage alerts efficiently in your SOC.

Tomorrow, I’ll guide you through integrating osTicket with your SOC tools, allowing you to automatically generate tickets for alerts and incidents, ensuring that your security operations are organized and accountable. Stay tuned!

### Day 25: Integrating OS Ticket with ELK Stack

Welcome to Day 25 of the 30-Day MYDFIR SOC Analyst Challenge! By the end of this tutorial, you’ll have successfully integrated **osTicket** into your SOC environment, allowing you to automatically create tickets for alerts generated in **Elastic Stack**. This setup will streamline your workflow and ensure efficient alert tracking. Let’s walk through the process in detail, step by step.

---

### Step 1: Access the OS Ticket Control Panel

1. **Login to osTicket**: Head to your osTicket control panel and log in.
2. **Navigate to Admin Panel**: Click the **Admin** link at the top-right corner.
3. **Create an API Key**:
   - Go to **Manage > API**.
   - Click **Add New API Key**.
   - Use the private IP of your Elastic server if it’s in the same VPC, or the public IP if they are in different VPCs.
   - Example IP: `172.31.3.x` (based on the VPC configuration in Vultr).
   - Enable **Can Create Tickets** and add an internal note for reference (e.g., “Elastic Connector for SOC Alerts”).
   - Click **Add Key** to generate the API key, and copy it to a safe location (like a Notepad file).

---

### Step 2: Configure Elastic Stack

1. **Login to Elastic Stack (Kibana)**:
   - Click the **hamburger menu** and navigate to **Stack Management**.
2. **Enable API Integration**:
   - If you’re using a free license, you need to enable a 30-day trial to unlock third-party API integrations.
   - Go to **Manage License** and activate the trial.
3. **Create a Webhook Connector**:
   - Under **Alerts and Insights**, select **Connectors**.
   - Click **Create Connector** and select **Webhook**.
   - Name your connector, e.g., "OS Ticket Connector".
   - Set the request type to **POST** and enter the URL: `http://<your-OS-ticket-IP>/api/tickets.xml`.
   - Add a header with `X-API-Key` and paste the key you copied from osTicket.
   - Click **Save and Test** to verify the connection.

---

### Step 3: Configure Payload and Test

1. **Define the Request Body**:
   - You’ll need a payload to send data from Elastic to osTicket. Here’s an example from osTicket's GitHub [page](https://github.com/osTicket/osTicket/blob/develop/setup/doc/api/tickets.md):
     ```xml
     <ticket>
       <subject>My DF 30-day Challenge - @YourHandle</subject>
       <message>Alert generated from Elastic</message>
       <name>Elastic Alert</name>
       <email>example@domain.com</email>
       <phone>555-5555</phone>
     </ticket>
     ```
   - Update the subject line to include “My DF 30-day Challenge” followed by your username.
   - Click **Run Test** to simulate sending an alert to OS Ticket.
2. **Verify Success**: Ensure the test confirms that the request was sent and processed correctly.

![[Screenshot 2024-09-25 at 5.20.27 PM 1.png]]


---

### Step 4: Troubleshoot Connectivity Issues

1. **Check Connectivity**:
   - Verify the IP configuration of your ELK server using the command `ip a` in PowerShell or SSH.
   - Ensure that you can ping the osTicket server using the private IP.
   - If there are issues, verify that the network settings on both servers are correct.
2. **Assign Static IP**:
   - If needed, assign a static private IP to your  osTicket server by going to **Control Panel > Network > Adapter Settings** on the osTicket server.
   - Re-run the test to check if connectivity is restored.

---

### Step 5: Final Test and Ticket Generation

1. **Retest the Connection**:
   - After confirming network connectivity, go back to Elastic Stack and re-run the **Save and Test** process.
2. **Check osTicket**:
   - Head back to the osTicket Agent Panel to verify if a ticket was successfully created based on the alert from Elastic Stack.

![[Screenshot 2024-09-25 at 5.22.09 PM 1.png]]

---

### Summary

Congratulations! You’ve now integrated osTicket into your SOC environment. With this integration, alerts from Elastic Stack can automatically generate tickets, enhancing your ability to track and manage security incidents.

---

**Recap of the 30-Day Challenge So Far**:
- **Day 1–10**: Setting up Elastic Stack, Kibana, and agents on Windows and Linux servers.
- **Day 11–20**: Creating alerts and dashboards for brute force detection and C2 activity.
- **Day 21–25**: Integrating osTicket for automated alert tracking.

In the next session, we’ll focus on investigating specific security alerts, starting with SSH brute force alerts. 

### Day 26: Investigating SSH Brute Force Alerts

Welcome to Day 26 of the 30-Day MYDFIR SOC Analyst Challenge! Today, we’re going to focus on investigating SSH brute-force alerts step by step. By the end of this guide, you will know how to dig deep into alerts, identify potential threats, and respond accordingly. 

---

### Step 1: Accessing the Alerts

1. **Log in to Elastic Security**: Navigate to the **Alerts** section under the security tab.
2. **Select the Alert**: You’ll see a list of alerts; select the most recent SSH brute-force alert.
3. **Review the Alert Description**: In this example, the alert is generated from multiple failed authentication attempts targeting the root account within a short time frame.

![[Screenshot 2024-09-26 at 1.07.51 PM.png]]

---

### Step 2: Exploring Elastic’s Timeline Feature

Although we won’t focus on Elastic’s **Timeline** feature today, it’s a powerful tool for investigations that lets you track event sequences and correlate activities. For now, we will investigate the alert directly.

---

### Step 3: Investigating the SSH Alert 

1. **Expand the Alert**: Review the details of the alert. It should provide information such as the source IP address and the targeted user (e.g., root).
2. **Key Points to Investigate**:
   - Is the source IP address known for malicious activity?
   - Has this IP targeted other user accounts?
   - Were any of the authentication attempts successful?
   - If successful, what actions followed?

These were the results I observed based on my lab setup:

![[Pasted image 20240928145327.png]]

---

### Step 4: IP Reputation Check

To assess whether the source IP address is suspicious, use external IP reputation tools:

1. **Check with AbuseIPDB**:
   - Copy the source IP from the alert.
   - Head over to **[AbuseIPDB](https://www.abuseipdb.com/)** and paste the IP to check its reputation.
   - If the IP has numerous reports, especially for brute force activity, it’s likely a known malicious source.
   
![[Pasted image 20240928150220.png]]
   
2. **Check with GreyNoise**:
   - Use **[GreyNoise](https://viz.greynoise.io/)** to gain additional context. GreyNoise can tag malicious behavior, like SSH brute force scanners or other automated tools associated with the IP.
   - In my case, you can see that "**77.73.131.144**" is known to be an SSH Bruteforcer.

![[Screenshot 2024-09-26 at 1.10.45 PM 1.png]]
   
Both tools can give you insights into whether the IP is commonly used in attacks.

---

### Step 5: Searching for Other Affected Users

It’s important to determine whether this IP has targeted other users:

1. **Go to Discover in Kibana**: Use the **Discover** feature to search for the IP address across logs.
2. **Filter by Time**: Set the time range to the past 30 days to check if other users were targeted.
3. **Review the Affected Users**: You may find other usernames the attacker attempted to brute force, providing a broader picture of the attack’s scope.

---

### Step 6: Checking for Successful Logins

Next, we need to check if any of the attacker’s attempts succeeded:

1. **Search for ‘Accepted’ Logins**: In SSH logs, successful login attempts are marked with the keyword “Accepted”. Search for this keyword in relation to the IP address.
2. **Check the Results**: If no successful logins are found, this indicates the brute-force attack was unsuccessful, but it’s still important to monitor closely for further attempts.

---

### Step 7: Finalizing the Investigation

Based on the investigation:

- **IP Reputation**: The source IP has been flagged as malicious.
- **Affected Users**: Multiple users were targeted.
- **Successful Logins**: No successful logins were found.

This suggests the attack posed a low risk but still warrants further monitoring. Document these findings for future reference.

---

### Step 8: Closing the Alert in a Ticketing System

For tracking and accountability, it’s crucial to log this investigation in a ticketing system like **OSTicket**:

1. **Assign the Ticket**: Assign the ticket to yourself or another analyst to avoid duplicate investigations.
2. **Document Your Findings**: Include the IP reputation check, affected users, and successful login check in the ticket.
3. **Close the Ticket**: Once everything is documented, mark the ticket as resolved, or leave it open for further monitoring.

---

### Step 9: Automating Ticket Creation

To streamline your process, you can set up Elastic to automatically create tickets in OS Ticket using webhooks:

1. **Edit Detection Rules**: Go to the **SSH Brute Force Rule** under Detection Rules.
2. **Add a Webhook**: Configure the webhook to send alerts to your ticketing system.
   
This automation saves time and ensures that all SSH brute-force alerts are logged and tracked.

---

### Summary

Today, we covered how to investigate an SSH brute-force alert by checking the IP reputation, searching for other affected users, and verifying if any login attempts were successful. By following these steps, you’ll be able to effectively investigate and respond to brute-force attacks as a SOC analyst.

Tomorrow, we’ll move on to investigating **RDP** alerts, building on the skills we’ve honed today. Stay tuned!

### Day 27: Investigating RDP Brute Force Alerts

Welcome to Day 27 of the MYDFIR-30 Day Challenge! Today, we’ll investigate **RDP Brute Force Alerts** using a step-by-step approach, similar to our process for SSH alerts. RDP brute force attacks can be frequent and harmful, so understanding how to respond to them is essential for a SOC Analyst. 

---

### Step 1: Accessing the Alerts

Log into your **SIEM** tool (such as Elastic Security) where the alerts are tracked.

- **Navigate to Alerts**: Click the **Hamburger Menu** and select the **Alerts** section.
- **Locate the Alert**: Find the most recent **RDP Brute Force alert** from the list of recent alerts.

![[Screenshot 2024-09-27 at 11.58.38 AM.png]]

---

### Step 2: Investigating the Source IP’s Reputation

To determine the risk level, investigate the **source IP** involved in the alert. Use **AbuseIPDB** and **GreyNoise** to check its reputation.

- **AbuseIPDB**: Input the source IP to see if it's been flagged for malicious behavior.

![[Screenshot 2024-09-27 at 12.55.32 PM.png]]
- **GreyNoise**: Use GreyNoise to check for scanning activity related to the IP.
-   In my case, you can see that "**100.15.133.81**" is not known to be an RDP Bruteforcer.

![[Screenshot 2024-09-27 at 12.53.40 PM.png]]

---

### Step 3: Investigating the RDP Alert

1. **Expand the Alert**: Review the details of the alert. It should provide information such as the source IP address and the targeted user (e.g., Administrator).
2. **Key Points to Investigate**:
   - Is the source IP address known for malicious activity?
   - Has this IP targeted other user accounts?
   - Were any of the authentication attempts successful?
   - If successful, what actions followed?

These were the results I observed based on my lab setup:

![[Screenshot 2024-09-30 at 1.45.28 PM.png]]

---

### Step 4: Checking for Successful Logins

Check if any of the brute-force login attempts were successful. Next, search for other user accounts that might have been targeted by this attack.

- **Go to Discover**: Use the **Discover** tool to filter logs for the source IP.
- **Search for Affected Users**: Check if other accounts besides **Administrator** were attacked.
- **Query for Event Code 4624**: Search for logs representing successful logins.
- **Check for Logins from the Source IP**: Ensure no logins were successful from the malicious IP.

---

### Step 5: Post-Login Activity (If Applicable)

If successful logins are detected, review post-login activities to detect suspicious behavior. If no successful logins were found, skip this step.

---

### Step 6: Finalizing the Investigation

Summarize the key findings:

- **IP Reputation**: Known for malicious behavior or scanning activity.
- **Affected Users**: Only the **Administrator** account was targeted.
- **Successful Logins**: None detected.

---

### Step 7: Closing the Alert in a Ticketing System

Track and close the alert in your **ticketing system**:

- **Assign the Ticket**: Assign the alert for tracking.
- **Document Findings**: Record the IP reputation, targeted users, and any successful logins.
- **Close the Ticket**: Once documented, mark the ticket as resolved.

---

### Step 8: Automating Ticket Creation

Set up automatic ticket creation for RDP brute-force alerts using your SIEM’s webhook integration just like we did above for SSH.

---

### Summary

Today, we investigated an **RDP Brute Force Alert**, checked the source IP’s reputation, reviewed targeted users, searched for successful logins, and logged our findings in a ticketing system. By following these steps, you can efficiently investigate RDP attacks and protect your network. Tomorrow, we’ll explore how to investigate our Mythic Agents alerts!

### Day 28: Investigating Mythic Agent Alerts

Welcome to Day 28 of the MYDFIR-30 Day Challenge! Today, we’re diving into investigating **Mythic Agent** alerts. Mythic agents can be highly covert, and understanding how to track and investigate their activities is key to keeping your systems secure. Let’s break down how to identify, investigate, and close Mythic Agent-related alerts in your SOC environment.

---

### Step 1: Accessing the Mythic Agent Dashboard

Start by logging into your **Elastic** instance and head over to the **Dashboard** section:

- **Go to the Hamburger Menu**: Click the menu and select the **Dashboard** you created for monitoring Mythic Agent activity.
- **Focus on Visualizations**: Specifically, we’ll look at visualizations for **process creation**, **process initialization**, and **Windows Defender being disabled**.

![[Screenshot 2024-09-28 at 3.05.18 PM.png]]

---

### Step 2: Investigating the Process Initialization

Check the **process initialization** for any unusual activity. You might notice a suspicious executable file located in an unexpected directory, like **C:\Users\Public\Downloads**.

- **Ask Critical Questions**: Why is an executable system file located in a public folder like **Downloads**? This could indicate malicious activity.
- **Look at the Ports**: In this case, observe the **IP addresses** and their corresponding **ports**. It’s suspicious if the same IP address communicates over different ports, like **80** and **9999**.

---

### Step 3: Searching for the Suspicious IP

Once you’ve identified the **suspicious IP address**, it’s time to dig deeper:

- **Head to Discover**: Use the **Discover** tool to search for this IP address.
- **Analyze Network Connections**: Look for any network connections associated with this IP and note the **ports** used.

This will help you determine if the agent has been communicating with an external command-and-control (C2) server.

---

### Step 4: Tracing the Process with ProcessGuid

To track specific processes:

- **Search for ProcessGuid**: Use **ProcessGuid** (a unique identifier) to trace back to the original **process** that initiated the suspicious activity.
- **Link to PowerShell**: You might find that **PowerShell** was executed from an unexpected location, indicating potential misuse.
  
By retracing the steps with **ProcessGuid**, you can build a timeline of how the Mythic Agent was executed and how it communicated with external sources.

---

### Step 5: Generating a Timeline

Now that you’ve identified suspicious processes, generate a **timeline**:

- **Track Related Events**: Use **ProcessGuid** to link related events, such as file downloads, PowerShell execution, and network connections.
- **Review File Names and Locations**: Look for any unfamiliar or suspicious files that were loaded during the Mythic Agent activity.

![[Screenshot 2024-09-29 at 9.00.28 AM 1.png]]

![[Screenshot 2024-09-29 at 9.00.54 AM.png]]
---

### Step 6: Investigating Files Downloaded by the Mythic Agent

Next, focus on the **files downloaded** by the Mythic Agent. You’ll want to investigate both **network telemetry** and **endpoint activity** to trace the downloaded files.

- **Check Network Telemetry**: Review any outbound connections that may have transferred data from your endpoint to an external server.
- **Analyze Endpoint Activity**: Look for any changes made to the system, such as file modifications or new files added.

---

### Step 7: Creating a Detection Rule for Mythic Agent Activity

Now that you’ve completed the investigation, let’s create a detection rule for **Mythic Agent activity**:

- **Go to Detection Rules**: Under **Security**, navigate to the **Detection Rules** section.
- **Create a New Rule**: Use a saved query or manually input criteria to detect Mythic Agent-related processes or network connections.
- **Set Alerts**: Configure the rule to trigger alerts whenever the Mythic Agent initiates suspicious activity, such as **PowerShell execution** or **unusual network connections**.

---

### Step 8: Closing the Investigation in OS Ticket

Finally, close the investigation by documenting your findings in **OS Ticket**:

- **Assign the Ticket**: Add comments detailing the investigation, including how you tracked the **Mythic Agent** and which processes were involved.
- **Resolve the Ticket**: Mark it as **resolved** once all necessary actions have been taken, such as blocking the IP or terminating the process.
  
---

### Summary

Today, we investigated **Mythic Agent** alerts by analyzing suspicious process activity, tracing connections via **ProcessGuid**, and creating detection rules for future monitoring. Using tools like **Elastic** and **OS Ticket**, we ensured the agent’s activity was tracked and documented. As we near the end of the challenge, these investigations are becoming crucial in building a complete SOC analyst skill set. Stay tuned for Day 29 where we configure Elastic Defend EDR on our ELK Stack!
\
### Day 29: Elastic Defend Setup

Welcome to Day 29 of the MYDFIR-30 Day Challenge! Today, we are setting up **Elastic Defend**, Elastic’s powerful Endpoint Detection and Response (EDR) solution. With Elastic Defend, we’ll enhance the security of our endpoints by detecting, responding to, and mitigating threats in real-time. This step is essential for fortifying our SOC environment.

---

### What is an EDR?

**Endpoint Detection and Response (EDR)** is a security solution that continuously monitors endpoints such as computers, servers, and mobile devices for potential threats. EDR serves several key functions:

- **Detect threats**: EDR identifies threats across the network, including advanced attacks.
- **Analyze threats**: It provides detailed information on how threats originated, where they’ve been, and their impact.
- **Respond to threats**: EDR can contain threats, prevent further damage, and even roll back the changes caused by malicious activity.
- **Detect zero-day and emerging threats**: EDR is capable of identifying previously unknown threats, including ransomware and advanced persistent threats (APTs).
- **Visibility and context**: EDR provides real-time visibility and actionable context for security teams and threat hunters.

---

### Step-by-Step Setup of Elastic Defend

#### Step 1: Log in to ELK and Start Integration

1. **Log in to ELK**: Using your credentials, log in to your ELK environment.
2. **Go to Integration**: Click the hamburger icon (menu) and navigate to **Integration** under the **Management** section.
3. **Select Elastic Defend**: Choose **Elastic Defend** from the list of integrations and click **Add Elastic Defend**.

---

#### Step 2: Configure Elastic Defend

1. **Configuration**: Name your integration and provide a brief description. Select the **environment** you want to protect (e.g., traditional endpoints).
2. **Host Selection**: Choose the existing host in your Fleet server setup, which we previously configured. 
3. **Policy Selection**: Select the **Windows policy** for complete EDR integration, then click **Save and Continue**.
4. **Deploy Changes**: Complete the integration by deploying the changes. The new Elastic Defend integration policy will be applied to your Windows server.

![[Screenshot 2024-09-29 at 9.00.04 AM.png]]

---

#### Step 3: Managing Endpoints

1. **Manage Endpoints**: Navigate to **Security** > **Manage** and select the **Endpoint** option. This section allows you to manage various endpoint actions, such as isolating hosts.
2. **Isolate Host**: To isolate the host, click on the three dots next to the server name and select **Isolate Host**.

---

#### Step 4: Testing the Setup

1. **Testing Malware Prevention**: 
    - On your **Windows server**, attempt to download a malicious payload from the **Mythic server**.
    - Elastic Defend should automatically block the download, detecting the file as malware.

![[Screenshot 2024-09-29 at 9.18.43 AM.png]]

---

#### Step 5: Viewing Logs

**Log Review**: 
    - Go to **Discover** in Kibana and search for "malware". 
    - Sort the logs by **newest to oldest** to view the most recent malware-related events. The logs will show details such as the **file name**, **file path**, and **file hash**.

---

#### Step 6: Reviewing Alerts

**Malware Prevention Alert**:
    - Go to **Security** > **Alerts** to see the **Malware Prevention Alert** triggered by Elastic Defend.
    - Expand the alert for detailed information about the file and actions taken, including file quarantine.

---

#### Step 7: Configuring Response Actions

**Creating Response Rules**:
    - Go to **Rules** under **Security** and edit the rule settings.
    - Under **Response Actions**, select **Elastic Defend** and set the response to **Isolate Host**.
    - Add a brief description, then save the changes.

---

#### Step 8: Testing Response Actions

**Testing Host Isolation**: 
    - Open **PowerShell** on your Windows server and attempt to download the payload from Mythic again.
    - The host will be isolated within seconds, confirming that your response action is working effectively.

---

### Summary

Today, we successfully set up **Elastic Defend** to enhance the security of our SOC environment. By integrating Elastic Defend, we now have a robust EDR solution that not only detects and prevents malware but also isolates compromised hosts, improving overall threat response. With this setup, our SOC is well-equipped to handle malware threats, providing real-time protection and detailed log visibility. 

We’re almost at the end of the **MYDFIR SOC Analyst Challenge**! Stay tuned for the final day, where we will summarize our 30-day journey and review the troubleshooting steps we’ve learned.

### Day 30: Common Troubleshooting Issues & Their Solutions

**🎉 Welcome to Day 30 of the MYDFIR 30-Day Challenge! 🎉**

Congratulations! You’ve made it to the final day of this challenge. Today, we’ll wrap up by focusing on some of the most common troubleshooting issues that arise during SOC operations and how to resolve them. Over the course of this journey, we’ve set up numerous systems, configured security tools, and worked through multiple investigations. Inevitably, there have been bumps along the way — firewall misconfigurations, connectivity issues, service interruptions, and more. 

Let’s walk through some of the common troubleshooting issues you might face in a SOC and how to tackle them effectively.

---

### Issue 1: Firewall Misconfigurations

One of the most frequent issues encountered when working with network security tools is firewall misconfigurations. Incorrect firewall settings can block essential services or allow unwanted traffic, leading to security gaps or operational downtime.

#### Solution:
1. **Validate Firewall Rules**:
   - Always ensure that both cloud and internal firewalls are properly configured.
   - Double-check that the correct ports are open for services like Elasticsearch (Port 9200), Kibana (Port 5601), and RDP (Port 3389).
   
   Example command for `ufw`:
   ```bash
   ufw allow 5601/tcp
   ufw allow 9200/tcp
   ```

2. **Narrow Access**:
   - Restrict access to specific IPs, especially for sensitive services like SSH (Port 22) and RDP (Port 3389).
   ```bash
   ufw allow from <trusted-IP> to any port 22
   ```

3. **Test Connectivity**:
   - Use `ping` and `traceroute` to check if the firewall is properly allowing traffic.
   ```bash
   ping <server-IP>
   traceroute <server-IP>
   ```

---

### Issue 2: Service Not Running or Failing to Start

Services like Elasticsearch, Kibana, and Fleet might fail to start after a reboot or configuration change. This could happen due to memory limitations, port conflicts, or improper configuration.

#### Solution:
1. **Check Service Status**:
   - Use `systemctl` to verify the status of critical services.
   ```bash
   systemctl status kibana.service
   systemctl status elasticsearch.service
   ```

2. **Restart Services**:
   - If a service is inactive, restart it:
   ```bash
   systemctl restart kibana.service
   ```

3. **Review Logs**:
   - Check the logs for more detailed information on why a service failed.
   ```bash
   journalctl -u kibana.service
   ```

4. **Monitor Resource Usage**:
   - Ensure that there’s enough memory and CPU to run the services by monitoring system resources.
   ```bash
   top
   ```

---

### Issue 3: Connectivity Problems Between Servers

In a distributed SOC environment, connectivity between different services and servers is vital. Sometimes, firewalls, incorrect IP assignments, or network settings can block communication between services like OS Ticket, Elastic, and Mythic.

#### Solution:
1. **Verify IP Address**:
   - Use `ipconfig` (on Windows) or `ip a` (on Linux) to check that the correct IP is assigned.

2. **Ping the Target Server**:
   - Ensure that the server can communicate with other endpoints by pinging the IP address:
   ```bash
   ping <other-server-IP>
   ```

3. **Review Firewall Rules**:
   - Confirm that the necessary ports are open on both the cloud firewall and the internal firewall.
   ```bash
   ufw allow <port-number>
   ```

---

### Issue 4: API Key or Authentication Failures

While integrating OS Ticket or any external system with Elastic, authentication issues, especially related to API keys or credentials, can arise.

#### Solution:
1. **Recheck API Key**:
   - Double-check that the API key was correctly copied and configured for the system.
   - In OS Ticket, go to the Admin panel and verify the API key settings.

2. **Test API Connection**:
   - Use a tool like Postman or `curl` to test the API connection and verify the response.
   ```bash
   curl -X POST http://<osticket-server-IP>/api/tickets.json -H "X-API-Key: <your-key>"
   ```

3. **Ensure Correct URL and Endpoint**:
   - Make sure the API endpoint is correctly specified in Elastic, along with the proper headers.

---

### Issue 5: Log Delays or Missing Data in Elastic

If Elastic isn’t ingesting logs correctly or logs appear delayed, it can severely impact your SOC’s ability to respond in real-time. This can be caused by overloaded servers, misconfigured log paths, or Elasticsearch not indexing properly.

#### Solution:
1. **Check Log Sources**:
   - Ensure that the correct log paths are configured, particularly for Sysmon, OS Ticket, and Fleet data sources.
   - Recheck the ingestion configurations under **Integrations** in the Elastic GUI.

2. **Check for Indexing Delays**:
   - Open **Kibana** and navigate to **Discover** to check for logs in real-time.
   - If there are delays, increase the refresh rate for indices.

3. **Monitor Elasticsearch Health**:
   - Use the following command to check the status of Elasticsearch:
   ```bash
   curl -XGET "localhost:9200/_cluster/health?pretty"
   ```

---

### Issue 6: Detection Rules Not Firing

After setting up detection rules in Elastic, there may be instances where alerts don’t fire as expected. This could be due to improper rule configuration or insufficient data.

#### Solution:
1. **Verify Rule Configuration**:
   - Check that the detection rule is configured correctly, with the right index patterns and query logic.
   
2. **Test the Rule**:
   - Use the **Test Rule** feature in Elastic to simulate the conditions for the rule and confirm that it triggers.

3. **Adjust Severity and Time Window**:
   - Ensure that the rule’s time window and severity levels align with the data being ingested.

---

### Summary

In the final stretch of the 30-Day SOC Analyst Challenge, we’ve highlighted some of the common issues that arise in SOC environments and provided solutions to resolve them. From firewall misconfigurations and service issues to connectivity problems and API failures, addressing these challenges is crucial for maintaining a secure and operational security infrastructure. With continuous monitoring and a methodical approach to troubleshooting, you can keep your SOC running smoothly and effectively respond to security threats.

Congratulations on completing the #MYDFIR 30-Day Challenge! Your journey in mastering SOC operations has equipped you with practical skills and knowledge essential for a successful career in cybersecurity. Keep learning, stay vigilant, and continue building on what you’ve accomplished!





