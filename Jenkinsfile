pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/virtualram-rgb/js-e2e-express-server.git'
            }
        }

        stage('Install dependencies') {
            steps {
                sh 'npm install'
                }
            }
        stage('build'){
            steps{
                 sh 'npm run build'
            }
        }
        stage ('Exec npm publish') {
            steps {
                rtNpmPublish (
                    tool: 'node', // Tool name from Jenkins configuration
                    path: "package.json",
                    deployerId: "NPM_DEPLOYER",
                    repo: "npmproject1-npm"
                )
            }
        }
        stage('Deploy') {
            steps {
             sh 'npm deploy'
            }
        }
    }
}
