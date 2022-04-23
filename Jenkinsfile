pipeline {
    agent any
    environment{
        NOMBRE='rossana'
        APELLIDO= 'suarez'
        APP_NAME= 'app-demo'
        REGISTRY ='roxsross12'
        DOCKER_HUB_LOGIN = 'docker-hub'
    }
    stages{
        stage ('checkout github'){
            steps{
                checkout scm
            }
        }  
        stage ('install dependencia'){
            steps{
                sh 'npm install'
            }
        }
        stage ('test'){
            steps{
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                sh 'npm run test'
            }
            }
        }
        stage ('build'){
            steps{
                sh 'docker build -t $APP_NAME .'
                sh 'docker images'
            }
        }
        stage ('tag version'){
            steps{
                sh 'docker tag $APP_NAME:latest $REGISTRY/$APP_NAME:latest'
                sh 'docker images'
            }
        stage ('deploy-push'){
            steps{
                sh 'docker login --username=$DOCKER_HUB_LOGIN_USR --password=$DOCKER_HUB_LOGIN_PSW'
            }   
        }
    }
}