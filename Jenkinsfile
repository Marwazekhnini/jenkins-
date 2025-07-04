stage('Clone Repository') {
    steps {
        echo '🔄 Cloning repository...'
        sh 'which git'
        sh 'git --version'
        sh 'ping -c 2 github.com || true'
        sh 'git clone https://github.com/your-username/dotnet.git || { echo "❌ GIT CLONE FAILED"; exit 1; }'
        dir('dotnet') {
            sh 'ls -la'
        }
    }
}
