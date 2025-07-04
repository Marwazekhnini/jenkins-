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
                sh 'git clone https://github.com/Marwazekhnini/jenkins-.git'
                dir('jenkins-') {
                    sh 'ls -la'
                }
            }
        }

        stage('Setup .NET SDK') {
            steps {
                echo '📦 Installing .NET SDK...'
                sh 'wget https://dot.net/v1/dotnet-install.sh -O dotnet-install.sh'
                sh 'chmod +x dotnet-install.sh'
                sh './dotnet-install.sh --version $DOTNET_VERSION || exit 1'
                sh '$HOME/.dotnet/dotnet --version'
            }
        }

        stage('Restore Dependencies') {
            steps {
                dir('jenkins-') {
                    echo '🔧 Restoring dependencies...'
                    sh 'PATH=$HOME/.dotnet:$PATH $HOME/.dotnet/dotnet restore > restore.log'
                    sh 'cat restore.log'
                }
            }
        }

        stage('Build') {
            steps {
                dir('jenkins-') {
                    echo '🏗️ Building...'
                    sh 'PATH=$HOME/.dotnet:$PATH $HOME/.dotnet/dotnet build --configuration Release > build.log'
                    sh 'cat build.log'
                }
            }
        }

        stage('Test') {
            steps {
                dir('jenkins-') {
                    echo '🧪 Testing...'
                    sh 'PATH=$HOME/.dotnet:$PATH $HOME/.dotnet/dotnet test --no-build > test.log'
                    sh 'cat test.log'
                }
            }
        }

        stage('Fake Deploy') {
            steps {
                dir('jenkins-') {
                    echo '🚀 Simulating deployment...'
                    sh 'echo "Deployment simulated!" > deploy.log'
                    sh 'cat deploy.log'
                }
            }
        }
    }

    post {
        success {
            echo '🎉 Pipeline succeeded!'
        }
        failure {
            echo '💥 Pipeline failed!'
        }
    }
}
