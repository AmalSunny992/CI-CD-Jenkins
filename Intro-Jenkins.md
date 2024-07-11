# Setting up Jenkins

## Objectives
- Understand what Jenkins is and why it is important
- Learn how to install Jenkins on your machine or a server
- Configure Jenkins for initial use

## Concepts
### What is Jenkins?
Jenkins is an open-source automation server that enables developers to build, test, and deploy their applications reliably and automatically. It is a widely used tool for implementing Continuous Integration (CI) and Continuous Delivery (CD) practices.

**Key Features of Jenkins:**

Extensibility: Jenkins supports hundreds of plugins to integrate with various tools in the CI/CD pipeline, including version control systems, build tools, test automation frameworks, and deployment tools.

Distributed Builds: Jenkins can distribute builds across multiple machines to speed up the build process and manage workloads efficiently.

Easy Configuration: Jenkins provides a web-based interface that simplifies the configuration of jobs and the overall system.

Active Community: Being open-source, Jenkins has a large and active community contributing to its development, which ensures regular updates and a wealth of plugins.

### Why Do We Need Jenkins?
Jenkins plays a crucial role in modern software development processes for several reasons:

#### Automation

Reduces Manual Effort: Jenkins automates repetitive tasks such as code compilation, testing, and deployment, reducing the need for manual intervention and minimizing human errors.

Consistent Processes: Automated processes ensure that every build follows the same steps, resulting in consistent and reliable outcomes.

#### Continuous Integration
Frequent Integration: Jenkins allows developers to frequently integrate their code changes into the main branch, triggering automated builds and tests. This helps in identifying issues early in the development cycle.

Quick Feedback: Automated testing provides immediate feedback on the code quality, enabling developers to address defects promptly.
Continuous Delivery/Deployment

Fast Releases: Jenkins automates the deployment process, allowing for faster and more reliable releases. It ensures that code changes are always in a deployable state.

Reduced Risks: By deploying smaller changes more frequently, Jenkins reduces the risk associated with large and infrequent releases.
Scalability

Distributed Builds: Jenkins can run multiple builds simultaneously on different nodes, making it scalable to handle large projects and multiple teams.

Load Management: Distributed builds help manage the load efficiently, reducing build times and improving productivity.

### Installing Jenkins
#### Prerequisites
Java: Jenkins requires Java to run. Ensure you have the Java Development Kit (JDK) installed.

System Requirements: Jenkins can run on Windows, macOS, or Linux. Ensure you have a compatible system.

### Installing Jenkins on Ubuntu/Debian
Update the system packages:

```bash
sudo apt update
```

**Install Java:**

```bash
#Update the system packages:
sudo apt update

#Install Java
sudo apt install fontconfig openjdk-17-jre -y

#Check Java Installation
java -version
openjdk version "17.0.8" 2023-07-18
OpenJDK Runtime Environment (build 17.0.8+7-Debian-1deb12u1)
OpenJDK 64-Bit Server VM (build 17.0.8+7-Debian-1deb12u1, mixed mode, sharing)
```

**Install Jenkins:**

```bash
# Add the Jenkins repository:
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

#Update the system packages again:
sudo apt-get update

#Install Jenkins:
sudo apt-get install jenkins -y

# Start Jenkins:
sudo systemctl start jenkins

# Enable Jenkins to start on boot:
sudo systemctl enable jenkins
```

**Accessing Jenkins:**
- Open a web browser and navigate to http://your_server_ip_or_domain:8080.
- You will see the "Unlock Jenkins" screen.

**Configuring Jenkins**

Unlock Jenkins:
- Jenkins installation generates an initial password located in /var/lib/jenkins/secrets/initialAdminPassword.

Retrieve the password:
```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

- Enter the password on the "Unlock Jenkins" screen.

Customize Jenkins:
- Choose "Install suggested plugins" on the "Customize Jenkins" page. This will install the most commonly used plugins.
- Alternatively, you can choose specific plugins to install by selecting "Select plugins to install."

Create First Admin User:
- Fill in the required details to create the first admin user.

Instance Configuration:
- Set the Jenkins URL. By default, it should be http://your_server_ip_or_domain:8080.

Start Using Jenkins:
- Click "Start using Jenkins."
- Basic Jenkins Configuration

Install Additional Plugins:
- Navigate to Manage Jenkins > Manage Plugins.
- Browse and install plugins as needed. Commonly used plugins include Git, GitHub, Pipeline, Docker, etc.

Configure Global Security:
- Navigate to Manage Jenkins > Configure Global Security.
- Set up authentication and authorization as per your requirements.

Set Up Nodes and Clouds:
- Navigate to Manage Jenkins > Manage Nodes and Clouds.
- Add new nodes to distribute the load and run jobs on multiple agents.

Configure Tools:
- Navigate to Manage Jenkins > Global Tool Configuration.
- Configure JDK, Git, Maven, and other tools needed for building projects.

### Example: Creating a Simple Job

Create a New Job:
- Click on "New Item" on the Jenkins dashboard.
- Enter an item name (e.g., HelloWorld) and select "Freestyle project".

Configure the Job:
- Under the "General" tab, provide a description for the job.
- Under the "Source Code Management" tab, configure the repository URL if using version control.
- Under the "Build" tab, add build steps. For example, you can add an "Execute shell" build step:

```bash
echo "Hello, World!"
```

Save and Build:
- Click "Save".
- Click "Build Now" to run the job.
- Check the build history and console output to see the results.

## Summary
In this lesson, you learned what Jenkins is, why it is important in modern software development, and how to install and configure it. Jenkins is a powerful tool for automating various aspects of software development, including building, testing, and deploying applications.