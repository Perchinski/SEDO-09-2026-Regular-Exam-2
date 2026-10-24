pipeline {
    agent any

    triggers {
        githubPush()
    }

    environment {
        DOTNET_CLI_TELEMETRY_OPTOUT = '1'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Restore') {
            steps {
                bat 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                bat 'dotnet build --no-restore --configuration Release'
            }
        }

        stage('Test') {
            steps {
                bat 'dotnet test --no-build --configuration Release --verbosity normal'
            }
        }
    }

    post {
        always {
            cleanWs()
        }
        success {
            echo 'Build and Tests completed successfully!'
        }
        failure {
            echo 'Build or Tests failed!'
        }
    }
}