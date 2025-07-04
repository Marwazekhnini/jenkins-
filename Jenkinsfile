pipeline {
    agent any

    environment {
        DOTNET_VERSION = '8.0'
        DOTNET_ROOT = "${HOME}/.dotnet"
        PATH = "${HOME}/.dotnet:${PATH}"
    }

    stages {

        stage('Clone Repository') {
            steps {
                echo '🔄 Cloning repository...'
                // 🛑 REPLACE THIS WITH YOUR REAL REPO URL if different
                sh 'git clone https://github.com/Marwazekhnini/jenkins-.git || exit 1'
                dir('jenkins-') {
                    sh 'ls -la'
                }
            }
        }

        stage('Install .NET SDK') {
            steps {
                echo '📦 Downloading .NET SDK...'
                sh 'wget https://dot.net/v1/dotnet-install.sh -O dotnet-install.sh'
                sh 'chmod +x dotnet-install.sh'
                sh './dotnet-install.sh --version $DOTNET_VERSION || exit 1'
                sh '$HOME/.dotnet/dotnet --version'
                echo '✅ .NET SDK is installed.'
            }
        }

        stage('Restore Dependencies') {
            steps {
                dir('jenkins-') {
                    echo '🔧 Restoring project dependencies...'
                    sh 'PATH=$HOME/.dotnet:$PATH $HOME/.dotnet/dotnet restore > restore.log || exit 1'
                    sh 'cat restore.log'
                }
            }
        }

        stage('Build Project') {
            steps {
                dir('jenkins-') {
                    echo '🏗️ Building the project...'
                    sh 'PATH=$HOME/.dotnet:$PATH $HOME/.dotnet/dotnet build --configuration Release > build.log || exit 1'
                    sh 'cat build.log'
                }
            }
        }

        stage('Run Tests') {
            steps {
                dir('jenkins-') {
                    echo '🧪 Running tests...'
                    sh 'PATH=$HOME/.dotnet:$PATH $HOME/.dotnet/dotnet test --no-build > test.log || exit 1'
                    sh 'cat test.log'
                }
            }
        }

        stage('Fake Deploy') {
            steps {
                dir('jenkins-') {
                    echo '🚀 Simulating deployment...'
                    sh 'echo "🎉 Deployment simulated!" > deploy.log'
                    sh 'cat deploy.log'
                }
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline finished successfully!'
        }
        failure {
            echo '❌ Pipeline failed. Check logs for details.'
        }
    }
}
