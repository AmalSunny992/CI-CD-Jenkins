# Automated Testing in Jenkins

## Objectives
- Learn how to set up automated tests in Jenkins
- Understand how to run tests in Jenkins Pipelines

## Concepts

### Setting up Automated Tests
Automated testing is a critical part of the Continuous Integration (CI) process. It ensures that code changes do not introduce new bugs and that the application behaves as expected. Automated tests can be integrated into Jenkins jobs to run tests automatically on code changes.

### Types of Automated Tests
**Unit Tests:** Test individual units or components of the software.

**Integration Tests:** Test the interaction between different components or systems.

**End-to-End Tests:** Test the entire application flow from start to finish.

#### Prerequisites
Ensure your project has a testing framework set up (e.g., JUnit for Java, pytest for Python, etc.).

Ensure the necessary dependencies for running tests are installed.

Example: Setting up Unit Tests for a Java Project

#### Create a Maven Project with JUnit Tests:

Ensure your pom.xml includes dependencies for JUnit:

```xml
<dependencies>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

#### Write a Simple JUnit Test:

Create a test class in the src/test/java directory:

```java
import org.junit.Test;
import static org.junit.Assert.assertEquals;

public class ExampleTest {
    @Test
    public void testAddition() {
        assertEquals(2, 1 + 1);
    }
}
```
### Running Tests in Jenkins Pipelines
Jenkins Pipelines can be used to automate the running of tests. Here’s how to integrate testing into your Jenkins Pipeline.

### Example: Running Tests in a Declarative Pipeline

- Create a New Pipeline Job:
    - Go to the Jenkins dashboard.
    - Click on "New Item".
    - Enter a name for your pipeline (e.g., TestPipeline).
    - Select "Pipeline" and click "OK".

- Configure the Pipeline:
    - In the pipeline configuration page, go to the "Pipeline" section.
    - Choose "Pipeline script" from the Definition drop-down.

**Write the Pipeline Script:**

```groovy
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-repo/your-project.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
    }

    post {
        always {
            junit '**/target/surefire-reports/*.xml'
        }
    }
}
```

- Save and Run:
    - Click "Save".
    - Click "Build Now" to run the pipeline.
    - Check the build history and console output to see the test results.

### Example: Running Tests in a Scripted Pipeline

- Create a New Pipeline Job:
    - Go to the Jenkins dashboard.
    - Click on "New Item".
    - Enter a name for your pipeline (e.g., ScriptedTestPipeline).
    - Select "Pipeline" and click "OK".

- Configure the Pipeline:
    - In the pipeline configuration page, go to the "Pipeline" section.
    - Choose "Pipeline script" from the Definition drop-down.

**Write the Pipeline Script:**

```groovy
Copy code
node {
    stage('Checkout') {
        git 'https://github.com/your-repo/your-project.git'
    }
    stage('Build') {
        sh 'mvn clean compile'
    }
    stage('Test') {
        sh 'mvn test'
    }
    stage('Report') {
        junit '**/target/surefire-reports/*.xml'
    }
}
```

- Save and Run:
    - Click "Save".
    - Click "Build Now" to run the pipeline.
    - Check the build history and console output to see the test results.

### Additional Configuration

**Configuring Test Reports**
JUnit Plugin: Ensure you have the JUnit plugin installed in Jenkins to process and display test results.

Archiving Test Results: Use the junit step to archive test results and make them available in the Jenkins interface.

**Handling Test Failures**
Post-Build Actions: Configure post-build actions to handle test failures (e.g., sending notifications, marking the build as unstable).

## Summary
In this lesson, you learned how to set up automated tests and run them in Jenkins Pipelines. Automated testing is a crucial part of CI/CD, ensuring that your code remains stable and functional as changes are introduced.