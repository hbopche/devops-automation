pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven"
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/hbopche/devops-automation.git']])

                // Run Maven on a Unix agent.
                sh "mvn clean install"
                sh "mvn clean package"
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build --build-arg JAR_FILE=target/devops-integration.jar -t harsh/myapp .'
                }
            }
        }
    }
}
