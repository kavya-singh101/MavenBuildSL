pipeline {
    agent any
    
    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                sh "mvn clean install -Dmaven.test.skip=true"
            }
        }
        
        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.war'
            }
        }
        
        stage('Deployment') {
            steps {
                deploy adapters: [
                    tomcat9(
                        url: 'http://15.206.151.1/8080/',
                        credentialsId: 'TomcatCreds'
                    )
                ], war: 'target/*.war', contextPath: 'app'
            }
        }
    }
}
