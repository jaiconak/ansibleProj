pipeline {
    agent any

    stages {
        
        stage ('Zip File') {
            steps {
                sh 'zip -r ansible-${BUILD_NUMBER}.ZIP * --exclude=Jenkinsfile'
                sh 'ls -l'
                sh 'echo "testing"'
            }
        }
    }

}