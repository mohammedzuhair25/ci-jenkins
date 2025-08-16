pipeline {
    agent any

    tools {
        // Refer to the JDK 1.8 installation configured in Jenkins Global Tool Configuration
        jdk 'jdk18'
        // Refer to the Maven installation configured in Jenkins Global Tool Configuration
    }

    stages {
        stage('Checkout') {
            steps {
                // Replace 'your-repository-url' with the actual URL of your Git repository
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Execute Maven clean and package goals
                sh 'mvn clean package' 
            }
        }

        stage('Test') {
            steps {
                // Execute Maven test goal (optional, can be integrated into 'Build' stage)
                sh 'mvn test' 
            }
        }

        stage('Archive Artifacts') {
            steps {
                // Archive the generated JAR/WAR file
                archiveArtifacts artifacts: 'target/*.jar, target/*.war', fingerprint: true
            }
        }
    }

    post {
        always {
            // Clean up workspace after build
            cleanWs() 
        }
        success {
            echo 'Maven project built successfully!'
        }
        failure {
            echo 'Maven project build failed.'
        }
    }
}