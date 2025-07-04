pipeline {
    agent any

    environment {
    DOTNET_ROOT = "${HOME}/.dotnet"
    PATH = "${HOME}/.dotnet:${env.PATH}"
}

    stages {

        stage('List Files (Validate Checkout)') {
            steps {
                echo '📁 Listing checked out files...'
                sh 'ls -la'
            }
        }

        stage('Setup .NET SDK') {
    steps {
        echo '📦 Installing .NET SDK 8.0.411...'
        sh '''
            wget https://dot.net/v1/dotnet-install.sh -O dotnet-install.sh
            chmod +x dotnet-install.sh
            ./dotnet-install.sh --version 8.0.411
            export PATH=$HOME/.dotnet:$PATH
            $HOME/.dotnet/dotnet --version
        '''
    }
}

        stage('Restore Dependencies') {
            steps {
                echo '🔧 Restoring dependencies...'
                sh 'PATH=$HOME/.dotnet:$PATH $HOME/.dotnet/dotnet restore > restore.log'
                sh 'cat restore.log'
            }
        }

        stage('Build') {
            steps {
                echo '🏗️ Building...'
                sh 'PATH=$HOME/.dotnet:$PATH $HOME/.dotnet/dotnet build --configuration Release > build.log'
                sh 'cat build.log'
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Testing...'
                sh 'PATH=$HOME/.dotnet:$PATH $HOME/.dotnet/dotnet test --no-build > test.log'
                sh 'cat test.log'
            }
        }

        stage('Fake Deploy') {
            steps {
                echo '🚀 Simulating deployment...'
                sh 'echo "Deployment simulated!" > deploy.log'
                sh 'cat deploy.log'
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
