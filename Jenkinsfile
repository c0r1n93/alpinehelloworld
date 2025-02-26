@Library('Jenkins-shared-library') _
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
                buildDockerImage()
                sh "docker rm -f ${CONTAINER_NAME}"
            }
        }
        stage('Run Docker Container') {
            steps {
                sh "docker run -d --name ${CONTAINER_NAME} -e PORT=80 -p 80:80 ${IMAGE_NAME}:${IMAGE_TAG}"
                sh 'sleep 5'
            }
        }
        stage('check Docker Container with return code') {
            steps {
                httpRequest(
                url: 'http://172.17.0.2:80',
                httpMode: 'GET',
                validResponseCodes: '200'
                )
            }
        }

        stage('Stop Docker Container') {
                steps {
                    sh "docker rm -f ${CONTAINER_NAME}"
                }
        }
    }
}
