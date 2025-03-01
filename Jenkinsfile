@Library('Jenkins-shared-library@main') _
pipeline {
    agent any

    parameters {
        string(name: 'containerName', defaultValue: 'alpine', description: 'the name of my container')
        string(name: 'imageName', defaultValue: 'alpine_image', description: 'the name of my container image')
        string(name: 'imageTag', defaultValue: '1.2', description: 'The version of my image')
        string(name: 'port', defaultValue: '80')
        string(name:'hostPort', defaultValue:'80')
        string(name:'containerPort', defaultValue:'80')
    }

    stages {
        stage('Build docker image') {
            steps {
                script {
                buildDockerImage("${params.imageName}", "${params.imageTag}")
                sh "docker rm -f ${CONTAINER_NAME}"
                }    
            }
        }
        stage('Run Docker Container') {
            steps {
                runDockerContainer("${params.containerName}", "${params.port}", "${params.hostPort}", "${params.containerPort}", "${params.imageName}", "${params.imageTag}")
            }
        }
        stage('check Docker Container with return code') {
            steps {
                checkDockerContainer()
            }
        }

        stage('Stop Docker Container') {
                steps {
                    stopDockerContainer("${params.containerName}")
                }
        }
    }
}
