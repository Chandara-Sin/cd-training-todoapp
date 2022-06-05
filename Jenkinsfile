pipeline {
    agent any
    stages {
        stage('Clone sources') {
            steps {
                git branch: 'master', credentialsId: 'github', url: 'https://github.com/Chandara-Sin/cd-training-todoapp.git'
            }
        }
        stage('confirm version') {
            steps {
                nodejs('NodeJS 18.3.0') {    // <- use node name you configured in  
                    sh 'node -v'
                    sh 'npm -v'
                }
            }
        }
        stage('install node packages') {
            steps {
                nodejs('NodeJS 18.3.0') {
                    sh 'npm install'
                }
            }
        }
         stage('Build') { 
            steps {
                sh 'node test' 
            }
        }
    }
}