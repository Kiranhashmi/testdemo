// Remove 'flag=true' (it's not being used and may cause parsing issues)
properties([
    disableConcurrentBuilds(),                     // Prevent multiple indexing runs
    pipelineTriggers([])                          // Disable automatic polling
])

pipeline {
    agent any
    options {
        skipDefaultCheckout()                     // Bypass default SCM checkout
        timeout(time: 15, unit: 'MINUTES')        // Prevent hangs
    }
    
    parameters {
        // Fixed parameter conflict (you had two VERSION params)
        choice(name: 'VERSION', choices:['1.1.0','1.2.0','1.3.0'], description:'')
        booleanParam(name:'executeTests', defaultValue: true, description:'')
    }

    environment {
        NEW_VERSION = '1.3.0'                     // Accessible across all stages
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM',
                    branches: [[name: env.BRANCH_NAME]],
                    extensions: [
                        [$class: 'CloneOption', shallow: true, depth: 1, noTags: true]
                    ],
                    userRemoteConfigs: [[url: env.GIT_URL]]
                ])
            }
        }

        stage('build') {
            steps {
                echo 'Building Project'
                echo "Building version ${NEW_VERSION}"
                echo 'successfully installed npm'
            }
        }

        stage('test') {
            when { expression { params.executeTests } }
            steps {
                echo 'Testing Project'
            }
        }

        stage('deploy') {
            steps {
                echo 'Deploying Project'
                echo "Deploying version ${params.VERSION}"
            }
        }
    }

    post {
        always {
            echo 'Post build condition running'
        }
        failure {
            echo 'Post Action if Build Failed'
        }
    }
}
