pipeline {
    agent {
        docker {
            image 'mcr.microsoft.com/dotnet/sdk:8.0'
        }
    }
    triggers {
        pollSCM '* * * * *'
    }
    stages {
        stage('Clone Repositories') {
            steps {
                echo "Cloning Repositories..."
                // Clone the repository containing the Jenkinsfile
                checkout scm

                // Clone the repository containing the tests
                sh 'git clone https://github.com/MimiXx-dev/App.E2ETests.git'
            }
        }
        stage('Build') {
            steps {
                echo "Building.."
                sh '''
                echo "doing build stuff.."
                '''
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
                sh '''
                echo "Running test.."
                cd App.E2ETests/tests
                dotnet test App.E2E.Tests.csproj
                '''
            }
        }
        stage('Deliver') {
            steps {
                echo 'Deliver....'
                sh '''
                echo "changes here to test automatic build.."
                '''
            }
        }
    }
}