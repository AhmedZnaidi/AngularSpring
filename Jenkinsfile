pipeline {
    agent any
    stages {
        stage('Build Angular App') {
            steps {
                dir('angular-app') {
                    sh 'npm install'
                    sh 'npm run build --prod'
                }
            }
        }
        stage('Build Spring Boot App') {
            steps {
                dir('spring-boot-app') {
                    sh './mvnw clean package -DskipTests'
                }
            }
        }
        stage('Build Docker Images') {
            steps {
                sh 'docker-compose build'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }
    post {
        always {
            echo 'Build and Deployment completed!'
        }
    }
}
