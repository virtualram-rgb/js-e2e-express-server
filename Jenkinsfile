pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/virtualram-rgb/js-e2e-express-server.git'
            }
        }

        stage('Install dependencies') {
            withSonarQubeEnv('sonar'){
                sh 'mvn install sonar:sonar'
            }
         }
        stage('Build and publish') {
            steps {
                sh 'npm run build',
                rtNpmPublish(
                    tool: 'node', // The NodeJS installation defined in Jenkins global configuration
                    specPath: 'package.json', // Path to your package.json file
                    args: '--registry=https://virtualhost.jfrog.io/artifactory/api/npm/npmproject1-npm/', // Optional: Specify your Artifactory registry URL if it differs from the default registry
                    deployerId: 'NPM_DEPLOYER', // The Artifactory server ID configured in Jenkins global configuration
                )
            }
        }

        stage('Deploy') {
            steps {
             'npm deploy'
            }
        }
    }
}
