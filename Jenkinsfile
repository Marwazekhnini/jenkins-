pipeline {
    agent any

    environment {
        DOTNET_VERSION = '8.0'
        DOTNET_ROOT = "${HOME}/.dotnet"
        PATH = "${DOTNET_ROOT}:${PATH}"
    }

    stages {
        stage('Clone Repository') {
            steps {
                echo '🔄 Cloning repository...'
                sh 'git clone https://github.com/your-username/dotnet.git'
                dir('dotnet') {
                    sh 'ls -la'
                }
            }
        }

        stage('Setup .NET SDK') {
            steps {
                echo '📦 Installing .NET SDK...'
                sh 'wget https://dot.net/v1/dotnet-install.sh -O dotnet-install.sh'
                sh 'chmod +x dotnet-install.sh'
                sh './dotnet-install.sh --version $DOTNET_VERSION'
                echo '✅ .NET SDK installed.'
            }
        }

        stage('Restore Dependencies') {
            steps {
                dir('dotnet') {
                    echo '🔧 Restoring project dependencies...'
                    sh '~/.dotnet/dotnet restore > restore.log'
                    sh 'cat restore.log'
                }
            }
        }

        stage('Build') {
            steps {
                dir('dotnet') {
                    echo '🏗️ Building the project...'
                    sh '~/.dotnet/dotnet build --configuration Release > build.log'
                    sh 'cat build.log'
                }
            }
        }

        stage('Test') {
            steps {
                dir('dotnet') {
                    echo '🧪 Running tests...'
                    sh '~/.dotnet/dotnet test --no-build --logger "trx" > test.log'
                    sh 'cat test.log'
                }
            }
        }

        stage('Fake Deploy') {
            steps {
                dir('dotnet') {
                    echo '🚀 Pretending to deploy the app...'
                    sh 'echo "Deployment simulated!" > deploy.log'
                    sh 'cat deploy.log'
                }
            }
        }
    }

    post {
        success {
            echo '🎉 Pipeline completed successfully!'
        }
        failure {
            echo '💥 Pipeline failed. Check logs above.'
        }
    }
}
