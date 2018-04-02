pipeline {
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -DskipTests clean package' 
            }
        }
        stage('Code Coverage') { 
            steps {
                sh 'mvn cobertura:cobertura' 
            }
        }
        stage('Test') { 
            steps {
                sh 'mvn clean test' 
            }
        }
        stage('Static Code Analysis') { 
            steps {
                sh 'mvn clean test' 
            }
        }
    }
}
