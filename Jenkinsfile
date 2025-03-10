pipeline {
    agent { label 'Jenkins-Agent' }

    tools {
        jdk 'Java17'  // Ensure this matches your Jenkins tool configuration
        maven 'maven3'  // Ensure this is correctly named in Jenkins
    }

    stages {
        stage("Cleanup Workspace") {
            steps {
                cleanWs()
            }
        }

        stage("Checkout from SCM") {
            steps {
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/vsaraths/register-app.git'
            }
        }

        stage("Build Application") {
            steps {
                sh "mvn clean package -DskipTests"  // Add -DskipTests to avoid running tests in build
            }
        }

        stage("Test Application") {
            steps {
                sh "mvn test"  // Runs unit tests
            }
        }
    }

    post {
        success {
            echo "Build and tests completed successfully!"
        }
        failure {
            echo "Build or tests failed! Check logs."
        }
    }
}

    
