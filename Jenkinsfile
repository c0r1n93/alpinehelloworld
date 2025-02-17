pipeline {
    agent any 
    parameters {
        string(name: 'CONTAINER_NAME', defaultValue: 'alpine_containe', description: 'Name of my container')
        string(name: 'IMAGE_NAME', defaultValue: 'alpine_image', description: 'Name of my container image')
        string(name: 'IMAGE_TAG', defaultValue: '1.1', description: 'version of my container image')
    }

    stages {   
        stage('Build Docker Image') {
            steps {
    
               sh 'docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .'
                
            }
        }
        stage('Run Docker Container') {
            steps {
            
                sh 'docker run -d --name ${CONTAINER_NAME} -e PORT=80 -p 80:80 ${IMAGE_NAME}:${IMAGE_TAG}'
                sh 'sleep 5'
                
            }
        }
        stage('check Docker Container with return code') {
            steps {
                httpRequest 'http://172.17.0.2:80'
                    httpmethod 'GET'
                    responseCode '200'
            }
        }
        stage('Stop Docker Container') {
                steps {
                    
                    sh 'docker stop ${CONTAINER_NAME}'
                    sh 'docker rm ${CONTAINER_NAME}'
                    
                }
            }
    }
}
