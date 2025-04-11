pipeline {
    agent any
    environment {
        APP_SERVER = 'ubuntu@18.222.21.205'         
        KEY_PATH = '/var/lib/jenkins/.ssh/my-key.pem'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                scp -i $KEY_PATH target/*.jar $APP_SERVER:/home/ubuntu/spring-app/
                ssh -i $KEY_PATH $APP_SERVER 'nohup java -jar /home/ubuntu/spring-app/*.jar > /home/ubuntu/app.log 2>&1 &'
                '''
            }
        }
    }
}

