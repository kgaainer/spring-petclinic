pipeline {
    agent any
    environment {
        APP_SERVER = 'ubuntu@18.222.21.205'         
        KEY_PATH = '/var/lib/jenkins/.ssh/my-key.pem'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/kgaainer/spring-petclinic.git'
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
                  scp -i $KEY_PATH target/*.war $APP_SERVER:/opt/tomcat/webapps/
                '''
            }
        }
    }
}

