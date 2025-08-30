pipeline {
    agent any

    tools {
        maven 'maven'   // Use the Maven name configured in Jenkins
  
    }
    stages {
        stage('Checkout') {
            steps {
               checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/kaustubh2949/maven-web-app.git']])
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv(credentialsId: 'sonar-token',installationName:'sonar') {
                    sh '''
                    mvn clean verify sonar:sonar \
                    -Dsonar.projectKey=maven-web-app \
                    -Dsonar.host.url=http://192.168.200.128:9000 \
                    -Dsonar.login=sqp_13b4312fa3284be173daf50b3ee3d5c26b38e9d2 '''
                    }
                }
            }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}