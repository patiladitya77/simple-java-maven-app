pipeline {
    agent any // Run this pipeline on any available Jenkins agent

    tools {
        // Tell Jenkins to use the Maven tool configured as 'maven-3.9.6'
        // We will configure this name in the Jenkins UI in the next part.
        maven 'maven-3.9.6'
    }

    stages {
        stage('Compile') {
            steps {
                // This command runs inside the container, so we use 'sh' (shell)
                echo 'Starting compilation...'
                sh 'mvn compile'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
        }

        stage('Build (Package)') {
            steps {
                echo 'Packaging application...'
                // 'clean package' cleans old builds and packages the code into a .jar file
                sh 'mvn clean package'
            }
            post {
                // This 'post' block runs after the steps in this stage
                success {
                    echo 'Build successful! Archiving artifacts...'
                    // Save the .jar file as a "build artifact"
                    archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
                }
            }
        }
    }
}