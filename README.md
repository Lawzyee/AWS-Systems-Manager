# Lab Project: Using AWS Systems Manager

## Overview
AWS Systems Manager is a powerful collection of tools that enable you to centralize operational data and automate tasks across your AWS resources. With Systems Manager, you can configure and manage Amazon Elastic Compute Cloud (EC2) instances, on-premises servers, virtual machines, and other resources at scale.

## Objectives
By completing this project, you will learn how to use Systems Manager to:

1. Verify configurations and permissions.
2. Run tasks on multiple servers.
3. Update application settings or configurations.
4. Access the command line of an instance securely.

---

## Tasks

### Task 1: Generate Inventory Lists for Managed Instances
In this task, you will use Fleet Manager to collect operating system information, application metadata, and other details from an EC2 instance.

#### Steps:
1. Open the **Systems Manager** console.
2. Navigate to **Node Management > Fleet Manager**.
3. Choose **Set up inventory** and configure the following:
   - **Name**: `Inventory-Association`
   - **Targets**: Manually select the managed instance.
4. Choose **Setup Inventory**.
5. Navigate to the **Node overview** and select the **Inventory** tab to review the instance's software and configuration.

Outcome: Successfully created an inventory association and verified instance configurations without using SSH.

---

### Task 2: Install a Custom Application Using Run Command
In this task, you will use Run Command to install the Widget Manufacturing Dashboard on an EC2 instance.

#### Steps:
1. Navigate to **Node Management > Run Command** in Systems Manager.
2. Search for the installation document (e.g., `Install Dashboard App`).
3. Configure the command:
   - Use default document version.
   - Select the managed instance as the target. 
   - Disable S3 bucket output.
4. Choose **Run** and wait for the overall status to change to **Success**.
5. Validate the installation:
   - Copy the public IP address of the EC2 instance.
   - Open the IP address in a browser to access the Widget Manufacturing Dashboard.

#### Screenshot of Inventory List:
![Inventory List Screenshot](Image%20output1.jpg)

Outcome: Installed and validated the custom application without using SSH.

---

### Task 3: Use Parameter Store to Manage Application Settings

Parameter Store, a capability of Systems Manager, provides secure, hierarchical storage for configuration data management and secrets management. You can store data such as passwords, database strings, and license codes as parameter values. You can store values as plain text or encrypted data. You can then reference values by using the unique name that you specified when you created the parameter.
In this task, you will configure an application setting using Parameter Store to activate a feature in the dashboard.

#### Steps:
1. Open the **Parameter Store** in the Systems Manager console.
2. Choose **Create parameter** and configure the following:
   - **Name**: `/dashboard/show-beta-features`
   - **Description**: `Display beta features`
   - **Value**: `True`
3. Refresh the dashboard in your browser to view the additional chart.

#### Screenshot of Widget Manufacturing Dashboard:
- **Before enabling the beta feature:**
  ![Widget Dashboard - Before](Image%20output2.jpg)

- **After enabling the beta feature:**
  ![Widget Dashboard - After](Image%20output2.jpg)

## Demonstration Video
[![Lab Demonstration Video](Video%20output.mp4)](Video%20output.mp4)

Outcome: Configured the application to check Parameter Store for settings and activate a beta feature.

---

### Task 4: Use Session Manager to Access Instances
In this task, you will use Session Manager to securely access an EC2 instance without using SSH.

#### Steps:
1. Navigate to **Node Management > Session Manager**.
2. Choose **Start session** and select the managed instance.
3. Run the following commands in the session:
   ```bash
   ls /var/www/html
   ```
   ```bash
   AZ=`curl -s http://169.254.169.254/latest/meta-data/placement/availability-zone`
   export AWS_DEFAULT_REGION=${AZ::-1}
   aws ec2 describe-instances
   ```
4. Verify the output, including application files and EC2 instance details.

Outcome: Securely accessed the instance and verified instance details using Session Manager.

---

## Conclusion
Congratulations! You have successfully:

- Verified configurations and permissions.
- Run tasks on multiple servers.
- Updated application settings or configurations.
- Accessed the command line of an instance securely using Session Manager.

AWS Systems Manager streamlines resource management, enhances security, and reduces the need for direct SSH access to instances.
