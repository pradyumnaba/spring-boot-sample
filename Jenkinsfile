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
            docker.image('mysql:latest').withRun('-e "MYSQL_ROOT_PASSWORD=root" -e "MYSQL_DATABASE=springbootsample"') { c ->
                docker.image('mysql:latest').inside("--link ${c.id}:db") {
                sh 'while ! mysqladmin ping -hdb --silent; do sleep 1; done'
                }

                docker.image('maven:3-alpine').withRun('-v /root/.m2:/root/.m2') { m ->
                docker.image('maven:3-alpine').inside("--link ${c.id}:db") {
                    sh 'mvn test'
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
