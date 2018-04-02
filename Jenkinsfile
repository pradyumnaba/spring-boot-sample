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
                git poll: true
                sh 'mvn -DskipTests clean package' 
            }
        }
        stage('Code Coverage') { 
            steps {
                sh 'mvn -DskipTests cobertura:cobertura' 
            }
        }
        stage('Test') { 
            steps {
                echo 'unit testing' 
            }
        }
        stage('Static Code Analysis') { 
            steps {
                echo 'static code analysis' 
            }
        }
    }
}
