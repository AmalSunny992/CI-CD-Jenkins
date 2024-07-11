# Deploying Applications with Jenkins

## Objectives
- Learn how to deploy applications to different environments using Jenkins
- Understand rollback strategies to handle deployment failures

## Concepts

### Deploying to Different Environments
Deploying applications involves moving your application code from the development environment to other environments, such as staging and production. Jenkins can automate this process, ensuring that deployments are consistent and repeatable.

#### Prerequisites
- Ensure your application is prepared for deployment (e.g., packaged, tested).
- Set up different environments (e.g., development, staging, production).

### Example: Deploying a Java Application

#### Pipeline Script for Deployment
- Create a New Pipeline Job:
    - Go to the Jenkins dashboard.
    - Click on "New Item".
    - Enter a name for your pipeline (e.g., DeployPipeline).
    - Select "Pipeline" and click "OK".

- Configure the Pipeline:
    - In the pipeline configuration page, go to the "Pipeline" section.
    - Choose "Pipeline script" from the Definition drop-down.

- Write the Pipeline Script:

```groovy
pipeline {
    agent any

    environment {
        DEV_SERVER = 'dev.example.com'
        STAGING_SERVER = 'staging.example.com'
        PROD_SERVER = 'prod.example.com'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-repo/your-project.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy to Development') {
            steps {
                deployApplication(DEV_SERVER)
            }
        }
        stage('Deploy to Staging') {
            steps {
                input message: 'Deploy to Staging?', ok: 'Deploy'
                deployApplication(STAGING_SERVER)
            }
        }
        stage('Deploy to Production') {
            steps {
                input message: 'Deploy to Production?', ok: 'Deploy'
                deployApplication(PROD_SERVER)
            }
        }
    }
}

def deployApplication(server) {
    sh """
    scp target/your-app.jar user@${server}:/path/to/deploy/
    ssh user@${server} 'systemctl restart your-app-service'
    """
}
```

- Save and Run:
    - Click "Save".
    - Click "Build Now" to run the pipeline.
    Follow the prompts to deploy to different environments.

### Rollback Strategies
Rollbacks are essential to quickly recover from deployment failures. A rollback strategy ensures that if a new deployment fails, the application can revert to the last known good state.

#### Types of Rollback Strategies

**Versioned Deployments:**
    - Keep multiple versions of the application deployed and switch between them.
    - Example: Blue-Green Deployment, Canary Releases.

**Backup and Restore:**
    - Before deploying a new version, back up the current version.
    - If the new deployment fails, restore from the backup.

**Database Rollbacks:**
    - Ensure database changes can be rolled back if necessary.
    - Use database migration tools (e.g., Flyway, Liquibase).
    - Example: Simple Rollback in Jenkins Pipeline

**Modify the Pipeline Script:**

Add a rollbackApplication function to the pipeline script.

```groovy
pipeline {
    agent any

    environment {
        DEV_SERVER = 'dev.example.com'
        STAGING_SERVER = 'staging.example.com'
        PROD_SERVER = 'prod.example.com'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-repo/your-project.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy to Development') {
            steps {
                deployApplication(DEV_SERVER)
            }
        }
        stage('Deploy to Staging') {
            steps {
                input message: 'Deploy to Staging?', ok: 'Deploy'
                deployApplication(STAGING_SERVER)
            }
        }
        stage('Deploy to Production') {
            steps {
                input message: 'Deploy to Production?', ok: 'Deploy'
                deployApplication(PROD_SERVER)
            }
        }
    }

    post {
        failure {
            rollbackApplication(PROD_SERVER)
        }
    }
}

def deployApplication(server) {
    sh """
    scp target/your-app.jar user@${server}:/path/to/deploy/
    ssh user@${server} 'systemctl restart your-app-service'
    """
}

def rollbackApplication(server) {
    sh """
    ssh user@${server} 'cp /path/to/deploy/your-app.jar.bak /path/to/deploy/your-app.jar'
    ssh user@${server} 'systemctl restart your-app-service'
    """
}
```
**Backup Before Deploying:**

Modify the deployApplication function to back up the current application version before deploying the new one.

```groovy
def deployApplication(server) {
    sh """
    ssh user@${server} 'cp /path/to/deploy/your-app.jar /path/to/deploy/your-app.jar.bak'
    scp target/your-app.jar user@${server}:/path/to/deploy/
    ssh user@${server} 'systemctl restart your-app-service'
    """
}

```

- Save and Test:
    - Click "Save".
    - Click "Build Now" to test the deployment and rollback.

## Summary
In this lesson, you learned how to deploy applications to different environments using Jenkins and implement rollback strategies to handle deployment failures. Automating deployments with Jenkins ensures consistency and reliability in your deployment process.