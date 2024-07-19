# Integrating Jenkins with GitHub

## Objectives
- Configure Jenkins to work with GitHub
- Set up GitHub Webhooks to trigger Jenkins builds

## Concepts
### Configuring Jenkins to Work with GitHub

#### Prerequisites
- Ensure you have Jenkins and Git installed on your system.
- Ensure you have a GitHub account with a repository to integrate with Jenkins.

#### Installing GitHub Plugin

1. Open Jenkins Dashboard:
    - Navigate to your Jenkins instance (e.g., http://your_server_ip_or_domain:8080).
![image](https://github.com/user-attachments/assets/a49fbe8e-558f-48fc-8227-352fa5cca944)

2. Manage Jenkins:
    - Click on "Manage Jenkins" from the Jenkins dashboard.
![image](https://github.com/user-attachments/assets/aa7b7931-078e-404b-9c9f-f1d3f83e6cad)

3. Manage Plugins:
    - Click on "Manage Plugins".
![image](https://github.com/user-attachments/assets/774b9ff2-a2a0-4e1e-add6-5d346d7cca73)

4. Available Tab:
    - Go to the "Available" tab.
    - Search for GitHub Plugin:
    - In the search box, type GitHub and select the "GitHub" plugin from the list.

5. Install GitHub Plugin:
    - Click "Install without restart" or "Download now and install after restart" based on your preference.
![image](https://github.com/user-attachments/assets/ec7a3523-676f-489d-9277-1a19e7027a01)

#### Configuring GitHub Integration

1. Create a New Item:
    - Go to the Jenkins dashboard.
    - Click on "New Item".
    - Enter a name for your job (e.g., GitHubIntegrationJob).
    - Select "Freestyle project" and click "OK".
![image](https://github.com/user-attachments/assets/22f182d8-51bb-4450-a05c-f536e36b59da)
![image](https://github.com/user-attachments/assets/b4e40a97-5c5c-4a69-87f0-28eafae085d1)

2. Configure Source Code Management:
    - In the job configuration page, go to the "Source Code Management" section.
    - Select "Git".
    - Enter your repository URL from GitHub (e.g., https://github.com/username/repository.git).
    - If your repository is private, configure the credentials.
![image](https://github.com/user-attachments/assets/a1874915-8809-41e3-9a50-bb47a5746954)
![image](https://github.com/user-attachments/assets/f13e9951-32ef-4712-9d89-b3a79f7e9196)
![image](https://github.com/user-attachments/assets/0f8eafbb-307c-4809-912e-268ef5c94f93)

3. Build Triggers:
    - Go to the "Build Triggers" section.
    - Check "GitHub hook trigger for GITScm polling".
![image](https://github.com/user-attachments/assets/566f0af6-56de-475e-8d4a-0d3d2589ad8e)

4. Add Build Step:
    - Go to the "Build" section.
    - Click on "Add build step" and select "Execute shell".
    - Enter the commands to build your project, for example:

```sh
echo "Building the project..."
```
![image](https://github.com/user-attachments/assets/66215ca1-1fc2-47a9-8266-90f1313dbba2)

5. Save the Job:
    - Click "Save".
    - Setting up GitHub Webhooks
![image](https://github.com/user-attachments/assets/1775ab65-fb45-4479-b4a2-4ec73f784e3d)

#### Create a Webhook in GitHub

1. Navigate to Your Repository:
    - Go to GitHub and navigate to the repository you want to integrate with Jenkins.

2. Settings:
    - Click on the "Settings" tab.
![image](https://github.com/user-attachments/assets/62dd3118-c559-4855-b980-53c931d48b17)

3. Webhooks:
    - In the left sidebar, click on "Webhooks".
![image](https://github.com/user-attachments/assets/b3aea708-f513-4521-b93c-d59b5f2fae57)

4. Add Webhook:
    - Click "Add webhook".
![image](https://github.com/user-attachments/assets/a850b482-3f45-4c4e-a743-6e9e81469c1f)

5. Configure Webhook:
    - Payload URL: Enter the Jenkins webhook URL. It should be http://your_jenkins_server_ip_or_domain:8080/github-webhook/.
    - Content Type: Select application/json.
    - Secret: (Optional) Enter a secret token for security.
    - Which events would you like to trigger this webhook?: Choose "Just the push event" or "Let me select individual events" based on your needs.
    - Active: Ensure the webhook is active.
![image](https://github.com/user-attachments/assets/eb31d1db-ca09-4df8-a359-225dbadc9d0c)

6. Add Webhook:
    - Click "Add webhook".

#### Testing the Webhook

1. Make a Change in Your Repository:
    - Push a commit to your repository.
![image](https://github.com/user-attachments/assets/5b50a8c2-31fe-4ab1-926c-238b3d722ddc)

2. Check Jenkins:
    - Go to Jenkins and verify that the job is triggered automatically by the push event.
![image](https://github.com/user-attachments/assets/dc0b0a22-02b6-448f-915c-17dc0dd15490)

### Example: Creating a Jenkins Pipeline Job with GitHub Integration
- **Create a New Pipeline Job:**
    - Go to the Jenkins dashboard.
    - Click on "New Item".
    - Enter a name for your pipeline (e.g., GitHubPipelineIntegration).
    - Select "Pipeline" and click "OK".

- **Configure Pipeline:**
    - In the pipeline configuration page, go to the "Pipeline" section.
    - Choose "Pipeline script from SCM".
    - Select "Git".
    - Enter your repository URL from GitHub.
    - Configure the credentials if the repository is private.
    - Enter the script path (e.g., Jenkinsfile).

- **Build Triggers:**
    - Go to the "Build Triggers" section.
    - Check "GitHub hook trigger for GITScm polling".

- **Save and Test:**
    - Click "Save".
    - Push a commit to the repository and verify that the pipeline job is triggered.

## Summary
In this lesson, you learned how to configure Jenkins to work with GitHub and set up GitHub webhooks to trigger Jenkins builds automatically. Integrating Jenkins with GitHub enhances your CI/CD pipeline by automating the build process based on changes in your repository.
