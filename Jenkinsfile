pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/UndertakerW/spring-petclinic.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn -B clean package'
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

        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh "${tool 'sonarqube'}/bin/sonar-scanner \
                    -D sonar.login=admin \
                    -D sonar.password=admin \
                    -D sonar.projectKey=spring-petclinic \
                    -D sonar.host.url=http://localhost:9000/"
                }
            }
        }
    }
    
}
