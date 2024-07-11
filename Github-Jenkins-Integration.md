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

2. Manage Jenkins:
    - Click on "Manage Jenkins" from the Jenkins dashboard.

3. Manage Plugins:
    - Click on "Manage Plugins".

4. Available Tab:
    - Go to the "Available" tab.
    - Search for GitHub Plugin:
    - In the search box, type GitHub and select the "GitHub" plugin from the list.

5. Install GitHub Plugin:
    - Click "Install without restart" or "Download now and install after restart" based on your preference.

#### Configuring GitHub Integration

1. Create a New Item:
    - Go to the Jenkins dashboard.
    - Click on "New Item".
    - Enter a name for your job (e.g., GitHubIntegrationJob).
    - Select "Freestyle project" and click "OK".

2. Configure Source Code Management:
    - In the job configuration page, go to the "Source Code Management" section.
    - Select "Git".
    - Enter your repository URL from GitHub (e.g., https://github.com/username/repository.git).
    - If your repository is private, configure the credentials.

3. Build Triggers:
    - Go to the "Build Triggers" section.
    - Check "GitHub hook trigger for GITScm polling".

4. Add Build Step:
    - Go to the "Build" section.
    - Click on "Add build step" and select "Execute shell".
    - Enter the commands to build your project, for example:

```sh
echo "Building the project..."
```

5. Save the Job:
    - Click "Save".
    - Setting up GitHub Webhooks

#### Create a Webhook in GitHub

1. Navigate to Your Repository:
    - Go to GitHub and navigate to the repository you want to integrate with Jenkins.

2. Settings:
    - Click on the "Settings" tab.

3. Webhooks:
    - In the left sidebar, click on "Webhooks".

4. Add Webhook:
    - Click "Add webhook".

5. Configure Webhook:
    - Payload URL: Enter the Jenkins webhook URL. It should be http://your_jenkins_server_ip_or_domain:8080/github-webhook/.
    - Content Type: Select application/json.
    - Secret: (Optional) Enter a secret token for security.
    - Which events would you like to trigger this webhook?: Choose "Just the push event" or "Let me select individual events" based on your needs.
    - Active: Ensure the webhook is active.

6. Add Webhook:
    - Click "Add webhook".

#### Testing the Webhook

1. Make a Change in Your Repository:
    - Push a commit to your repository.

2. Check Jenkins:
    - Go to Jenkins and verify that the job is triggered automatically by the push event.

### Example: Creating a Jenkins Pipeline Job with GitHub Integration
**Create a New Pipeline Job:**
    - Go to the Jenkins dashboard.
    - Click on "New Item".
    - Enter a name for your pipeline (e.g., GitHubPipelineIntegration).
    - Select "Pipeline" and click "OK".

**Configure Pipeline:**
    - In the pipeline configuration page, go to the "Pipeline" section.
    - Choose "Pipeline script from SCM".
    - Select "Git".
    - Enter your repository URL from GitHub.
    - Configure the credentials if the repository is private.
    - Enter the script path (e.g., Jenkinsfile).

**Build Triggers:**
    - Go to the "Build Triggers" section.
    - Check "GitHub hook trigger for GITScm polling".

**Save and Test:**
- Click "Save".
- Push a commit to the repository and verify that the pipeline job is triggered.

## Summary
In this lesson, you learned how to configure Jenkins to work with GitHub and set up GitHub webhooks to trigger Jenkins builds automatically. Integrating Jenkins with GitHub enhances your CI/CD pipeline by automating the build process based on changes in your repository.