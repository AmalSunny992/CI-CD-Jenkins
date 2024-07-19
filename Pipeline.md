# Jenkins Pipelines

## Objectives
- Understand the basics of Jenkins Pipelines
- Learn how to write and configure Pipeline jobs in Jenkins

## Concepts

### Introduction to Jenkins Pipelines
Jenkins Pipelines are a suite of plugins that support implementing and integrating continuous delivery pipelines into Jenkins. A pipeline is a series of events or jobs which are interlinked to perform a sequence of operations, such as building, testing, and deploying code.

### Benefits of Jenkins Pipelines
Code as Configuration: Pipelines are defined in code, making them easy to version, review, and maintain.

Complex Workflows: Pipelines can handle complex build workflows, including parallel and sequential stages.

Error Handling: Built-in support for handling errors and retrying steps.

Extensibility: Easily extendable with plugins and shared libraries.

### Types of Pipelines
Declarative Pipeline: Provides a simplified, predefined syntax for defining a pipeline. It's easier to read and write.

Scripted Pipeline: Uses Groovy code for defining the pipeline. It's more flexible and powerful but can be more complex to write.

### Writing and Configuring Pipeline Jobs

#### Creating a Simple Declarative Pipeline

**Create a New Pipeline Job:**
- Go to the Jenkins dashboard.
- Click on "New Item."
- Enter a name for your pipeline (e.g., MyFirstPipeline).
- Select "Pipeline" and click "OK."

**Define the Pipeline:**
- In the pipeline configuration page, go to the "Pipeline" section.
- Choose "Pipeline script" from the Definition drop-down.

**Write the Pipeline Script:**

```groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // Add your build commands here
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                // Add your test commands here
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
                // Add your deploy commands here
            }
        }
    }
}
```

**Save and Run:**
- Click "Save."
- Click "Build Now" to run the pipeline.
- Check the build history and console output to see the results.

#### Creating a Scripted Pipeline

**Create a New Pipeline Job:**
- Go to the Jenkins dashboard.
- Click on "New Item."
- Enter a name for your pipeline (e.g., MyScriptedPipeline).
- Select "Pipeline" and click "OK."

**Define the Pipeline:**
- In the pipeline configuration page, go to the "Pipeline" section.
- Choose "Pipeline script" from the Definition drop-down.


**Write the Pipeline Script:**

```groovy
node {
    stage('Build') {
        echo 'Building...'
        // Add your build commands here
    }
    stage('Test') {
        echo 'Testing...'
        // Add your test commands here
    }
    stage('Deploy') {
        echo 'Deploying...'
        // Add your deploy commands here
    }
}
```

**Save and Run:**
- Click "Save."
- Click "Build Now" to run the pipeline.
- Check the build history and console output to see the results.


### Pipeline Syntax
**pipeline:** Defines the pipeline.

**agent:** Specifies where the pipeline or a specific stage runs.

**stages:** Contains a sequence of one or more stage directives.

**stage:** Defines a stage in the pipeline.

**steps:** Contains a sequence of one or more step directives.

### Example: Parallel Stages

You can also run stages in parallel to speed up the pipeline execution.

```groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
        stage('Test') {
            parallel {
                stage('Unit Tests') {
                    steps {
                        echo 'Running unit tests...'
                    }
                }
                stage('Integration Tests') {
                    steps {
                        echo 'Running integration tests...'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        }
    }
}
```

### Example: Handling Failures
Jenkins pipelines provide mechanisms for handling failures and performing cleanup actions.

```groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // Simulating a build failure
                sh 'exit 1'
            }
        }
    }

    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if the build succeeds'
        }
        failure {
            echo 'This will run only if the build fails'
        }
        unstable {
            echo 'This will run only if the build is unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
        }
    }
}
```

### Configuring Pipeline Jobs

**Configure SCM:**

In the pipeline configuration, you can specify a repository URL to pull the pipeline script from version control.
Select the "Pipeline script from SCM" option and configure your repository settings.

**Environment Variables:**

You can define environment variables in the pipeline script.

```groovy
pipeline {
    agent any

    environment {
        MY_VAR = 'some_value'
    }

    stages {
        stage('Example') {
            steps {
                echo "Environment variable value: ${env.MY_VAR}"
            }
        }
    }
}
```

**Triggers:**

Configure triggers to automatically run the pipeline based on certain events (e.g., SCM changes, periodic triggers).

In the pipeline configuration, go to the "Build Triggers" section and configure the desired triggers.

## Summary
In this lesson, you learned about Jenkins Pipelines, their benefits, and how to write and configure both Declarative and Scripted Pipeline jobs. Jenkins Pipelines provide a powerful way to automate complex workflows and improve the efficiency of your CI/CD processes.
