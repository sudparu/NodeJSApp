pipeline{
    agent any
    options{
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
    environment{
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
        APP_NAME = 'nodejs'
        USER_NAME='sudparu'
    }
    stages{
        stage('Build'){
            steps{
                sh 'docker build -t $USER_NAME/$APP_NAME .'
            }
        }
        stage('Login'){
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin' 
            }
        }
        stage('Push'){
            steps{
                sh 'docker push $USER_NAME/$APP_NAME'
            }
        }
        stage('Run the image locally'){
            steps{
               sh 'docker run -p 9000:3000 $USER_NAME/$APP_NAME'
            }
        }
    }
}
