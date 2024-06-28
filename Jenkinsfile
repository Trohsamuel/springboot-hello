pipeline {
    agent any 
    tools {
        maven "3.8.7"
    }
    stages {
        stage('Compile and Clean') { 
            steps {
                // Exécuter Maven sur un agent Unix.
                sh "mvn clean compile"
            }
        }
        stage('Deploy') { 
            steps {
                sh "mvn package"
            }
        }
        stage('Build Docker image') {
            steps {
                echo "Hello Java Express"
                sh 'ls'
                sh 'docker build -t trohsamuel/docker_jenkins_springboot:${BUILD_NUMBER} .'
            }
        }
        stage('Docker Login') {
            steps {
                withCredentials([string(credentialsId: 'DockerId', variable: 'Dockerpwd')]) {
                    sh "docker login -u trohsamuel -p Admin61*Bonjour@2024"
                }
            }                
        }
        stage('Docker Push') {
            steps {
                sh 'docker push trohsamuel/docker_jenkins_springboot:${BUILD_NUMBER}'
            }
        }
        stage('Docker Deploy') {
            steps {
                sh 'docker run -itd -p 8081:8080 trohsamuel/docker_jenkins_springboot:${BUILD_NUMBER}'
            }
        }
        stage('Archiving') { 
            steps {
                archiveArtifacts '**/target/*.jar'
            }
        }
    }
}
