pipeline {
    agent any
    
    triggers {
        pollSCM('*/1 * * * *')
    }
    
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
            junit 'target/surefire-reports/*.xml'
        }
    }
}
