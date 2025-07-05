pipeline {
    agent any

    environment {
    DOTNET_VERSION = '8.0.411'
    DOTNET_ROOT = "${HOME}/.dotnet"
    PATH = "${DOTNET_ROOT}:${PATH}"
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
            cd dotnet-minimal-web-api-example/DotNetMinimalAPIDemo
            dotnet --version
            dotnet restore MinimalAPIDemo.sln
        '''
    }
}

        stage('Build') {
    steps {
        echo '🏗️ Building project...'
        sh '''
            export PATH=$HOME/.dotnet:$PATH
            cd dotnet-minimal-web-api-example/DotNetMinimalAPIDemo
            dotnet build --configuration Release
        '''
    }
}

        stage('Test') {
    steps {
        echo '🧪 Running tests...'
        sh '''
            export PATH=$HOME/.dotnet:$PATH
            cd Downloads/dotnet-minimal-web-api-example/DotNetMinimalAPIDemo
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
        stage('Debug Workspace') {
           steps {
              sh 'pwd && ls -R'
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
