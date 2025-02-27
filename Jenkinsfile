@Library('Jenkins-shared-library@v1.2') _
pipeline {
    agent any

    parameters {
        string(name: 'CONTAINER_NAME', defaultValue: 'alpine', description: 'the name of my container')
        string(name: 'IMAGE_NAME', defaultValue: 'alpine_image', description: 'the name of my container image')
        string(name: 'IMAGE_TAG', defaultValue: '1.2', description: 'The version of my image')
    }

    stages {
        stage('Build docker image') {
            steps {
                script {
                buildDockerImage()
                sh "docker rm -f ${CONTAINER_NAME}"
                }    
            }
        }
        stage('Run Docker Container') {
            steps {
                runDockerContainer()
            }
        }
        stage('check Docker Container with return code') {
            steps {
                checkDockerContainer()
            }
        }

        stage('Stop Docker Container') {
                steps {
                    stopDockerContainer()
                }
        }
    }
}
