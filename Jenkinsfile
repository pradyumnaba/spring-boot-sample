pipeline {
    agent any
    stages {
        stage('checkout code') {
            steps {
                checkout scm
            }        
        }               
        stage('build code') {
            steps {
                mvn clean install
            }        
        }               

    }
}
