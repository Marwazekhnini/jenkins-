pipeline {
    agent any

    environment {
        DOTNET_VERSION = '8.0.411'
        DOTNET_ROOT = "${HOME}/.dotnet"
        PATH = "${DOTNET_ROOT}:${PATH}"
    }

    stages {
        stage('Checkout SCM') {
            steps {
                echo '📥 Cloning repository...'
                checkout scm
            }
        }

        stage('Setup .NET SDK') {
            steps {
                echo '📦 Installing .NET SDK...'
                sh '''
                    wget https://dot.net/v1/dotnet-install.sh -O dotnet-install.sh
                    chmod +x dotnet-install.sh
                    ./dotnet-install.sh --version $DOTNET_VERSION --install-dir $DOTNET_ROOT
                '''
            }
        }

        stage('Debug Workspace') {
            steps {
                echo '🔍 Debugging workspace...'
                sh '''
                    echo "📁 Current Working Directory:"
                    pwd

                    echo "📂 All Directories:"
                    find . -type d || true

                    echo "📃 Current Folder Contents:"
                    ls -la

                    echo "🌲 Tree structure (if tree installed):"
                    command -v tree && tree || echo "tree not installed"
                '''
            }
        }

        stage('Restore Dependencies') {
            steps {
                echo '🔧 Restoring dependencies...'
                sh '''
                    export PATH=$DOTNET_ROOT:$PATH
                    cd DotNetMinimalAPIDemo
                    dotnet --version
                    dotnet restore
                '''
            }
        }

        stage('Build') {
            steps {
                echo '🏗️ Building project...'
                sh '''
                    export PATH=$DOTNET_ROOT:$PATH
                    cd DotNetMinimalAPIDemo
                    dotnet build --configuration Release
                '''
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Running tests...'
                sh '''
                    export PATH=$DOTNET_ROOT:$PATH
                    cd DotNetMinimalAPIDemo
                    dotnet test --no-build
                '''
            }
        }

        stage('Fake Deploy') {
            steps {
                echo '🚀 Simulating deployment...'
                sh 'echo "Deployment simulated!"'
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
