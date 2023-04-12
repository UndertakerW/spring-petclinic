pipeline {
    agent any
    
    tools {
        maven 'maven'
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/UndertakerW/spring-petclinic.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn -B clean install'
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn -B test'
            }
        }

        stage('Results') {
            steps {
                junit '**/target/surefire-reports/TEST-*.xml'
                archiveArtifacts 'target/*.jar'
            }
        }

        stage('SonarQube') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh "mvn sonar:sonar \
                    -D sonar.login=${params.SONARQUBE_USER} \
                    -D sonar.password=${params.SONARQUBE_PASSWORD} \
                    -D sonar.projectKey=spring-petclinic \
                    -D sonar.host.url=http://${params.SONARQUBE_IP}:9000/ \
                    -D sonar.sources=src/main/java/ \
                    -D sonar.tests=src/test/java/ \
                    -D sonar.java.binaries=target/classes"
                }
            }
        }
    }
    
}
