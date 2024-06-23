pipeline {
    agent {
        docker {
            image 'mcr.microsoft.com/dotnet/sdk:8.0'
            args '-v /var/run/docker.sock:/var/run/docker.sock -v $HOME/.m2:/root/.m2 -v $HOME/.dotnet:/root/.dotnet'
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

                // Clone or update the repository containing the tests
                script {
                    def repoDir = "App.E2ETests"
                    if (fileExists(repoDir)) {
                        echo "Repository already exists, updating..."
                        sh "cd ${repoDir} && git pull"
                    } else {
                        echo "Cloning repository..."
                        sh "git clone https://github.com/MimiXx-dev/App.E2ETests.git ${repoDir}"
                    }
                }
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