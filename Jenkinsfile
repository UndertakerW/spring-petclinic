pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/UndertakerW/spring-petclinic.git'
            }
        }
        
        stage('Build') {
            steps {
                sh '/opt/maven/bin/mvn -B clean package'
            }
        }
        
        stage('Test') {
            steps {
                sh '/opt/maven/bin/mvn -B test'
            }
        }
    }
    
    post {
        always {
            junit 'target/site/jacoco/jacoco.xml'
        }
    }
}
