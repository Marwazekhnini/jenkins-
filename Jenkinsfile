pipeline {
    agent any

    environment {
        DOTNET_VERSION = '8.0.411'
        DOTNET_ROOT = "${HOME}/.dotnet"
    }

    stages {
        stage('Setup .NET SDK') {
            steps {
                echo '📦 Installing .NET SDK...'
                sh '''
                    wget https://dot.net/v1/dotnet-install.sh -O dotnet-install.sh
                    chmod +x dotnet-install.sh
                    ./dotnet-install.sh --version $DOTNET_VERSION
                '''
            }
        }

        stage('Restore Dependencies') {
            steps {
                echo '🔧 Restoring dependencies...'
                sh '''
                    export PATH=$HOME/.dotnet:$PATH
                    dotnet --version
                    dotnet restore
                '''
            }
        }

        stage('Build') {
            steps {
                echo '🏗️ Building project...'
                sh '''
                    export PATH=$HOME/.dotnet:$PATH
                    dotnet build --configuration Release
                '''
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Running tests...'
                sh '''
                    export PATH=$HOME/.dotnet:$PATH
                    dotnet test --no-build
                '''
            }
        }

        stage('Fake Deploy') {
            steps {
                echo '🚀 Simulating deployment...'
                sh '''
                    echo "Deployment simulated!"
                '''
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
