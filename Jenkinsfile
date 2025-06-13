pipeline {
    agent any

    tools {
        maven 'Maven'  // Replace this with the exact name from Jenkins > Global Tool Config
    }

    parameters {
        choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: 'Version to deploy')
        booleanParam(name: 'executeTests', defaultValue: true, description: 'Run test stage?')
    }

    environment {
        NEW_VERSION = '1.3.0'
    }

    stages {
        stage('Build') {
            steps {
                echo '🔨 Building Project'
                echo "Using Maven Version: ${tool 'Maven 3.9'}"
                echo "Building version ${NEW_VERSION}"
                bat 'mvn clean install'
            }
        }

        stage('Test') {
            when {
                expression { params.executeTests }
            }
            steps {
                echo '🧪 Running Tests'
                bat 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo '🚀 Deploying Project'
                echo "Deploying version ${params.VERSION}"
                // Simulate deployment step
                bat 'echo Deploying version ${params.VERSION}'
            }
        }
    }

    post {
        always {
            echo '📦 Post build condition running'
        }
        failure {
            echo '❌ Post action: Build Failed'
        }
    }
}
