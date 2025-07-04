pipeline {
    agent any

    environment {
    DOTNET_VERSION = '8.0.411'
    DOTNET_ROOT = "${HOME}/.dotnet"
    // No PATH modification here
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
        dir('jenkins-') {
            echo '🔧 Restoring dependencies...'
            sh '''
                export PATH=$HOME/.dotnet:$PATH
                dotnet restore > restore.log
                cat restore.log
            '''
        }
    }
}


        stage('Build') {
    steps {
        dir('jenkins-') {
            echo '🏗️ Building...'
            sh '''
                export PATH=$HOME/.dotnet:$PATH
                dotnet build --configuration Release > build.log
                cat build.log
            '''
        }
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
