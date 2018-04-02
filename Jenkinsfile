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
                sh 'mvn -DskipTests cobertura:cobertura' 
            }
        }
        stage('Setup DB and Test') { 
            steps {
                script{
                   docker.image('mysql:5').withRun('-e "MYSQL_ROOT_PASSWORD=my-secret-pw" -p 3306:3306') { c ->
                   /* Wait until mysql service is up */
                   sh 'while ! mysqladmin ping -h0.0.0.0 --silent; do sleep 1; done'
                   /* Run some tests which require MySQL */
                }
             }
    }
           
        }        
        
        stage('Static Code Analysis') { 
            steps {
                echo 'static code analysis' 
            }
        }


    }
}
