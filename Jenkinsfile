pipeline {
  agent any

  parameters {
    string(name: 'CONTAINER_NAME', defaultValue: 'alpine', description: 'the name of my container')
    string(name: 'IMAGE_NAME', defaultValue: 'alpine_image', description: 'the name of my container image')
    string(name: 'IMAGE_TAG', defaultValue: '1.1', description: 'The version of my image')
  }

  stages {
    stage('Build docker image') {
      steps {
        sh 'docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .'
        sh 'docker rm -f ${CONTAINER_NAME}'
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
                    
                
                    sh 'docker rm -f ${CONTAINER_NAME}'
                    
                }
            }
  }
    
}