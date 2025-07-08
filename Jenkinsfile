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

                    echo "🧾 .csproj and .sln files:"
                    find . -name "*.csproj" -o -name "*.sln"

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

                    # Replace with your actual project file name if needed
                    dotnet restore DotNetMinimalAPIDemo.csproj
                '''
            }
        }

        stage('Build') {
            steps {
                echo '🏗️ Building project...'
                sh '''
                    export PATH=$DOTNET_ROOT:$PATH
                    cd DotNetMinimalAPIDemo
                    dotnet build DotNetMinimalAPIDemo.csproj --configuration Release
                '''
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Running tests...'
                sh '''
                    export PATH=$DOTNET_ROOT:$PATH
                    cd DotNetMinimalAPIDemo
                    dotnet test DotNetMinimalAPIDemo.csproj --no-build
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
