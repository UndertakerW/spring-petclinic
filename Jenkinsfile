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
                    sh "${tool 'sonarqube'}/bin/sonar-scanner \
                    -D sonar.login=admin \
                    -D sonar.password=admin \
                    -D sonar.projectKey=spring-petclinic \
                    -D sonar.host.url=http://${SONARQUBE_IP}:9000/ \
                    -D sonar.sources=src/main/java/ \
                    -D sonar.java.binaries=target/classes"
                }
            }
        }
    }
    
}
