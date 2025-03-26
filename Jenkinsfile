pipeline {
    agent any

    stages {
        
        stage ('Zip File') {
            steps {
                sh 'zip -r ansible-${BUILD_NUMBER}.zip * --exclude=Jenkinsfile'
                sh 'ls -l'
                sh 'echo "testing!"'
            }
        }

        stage ('Upload to JFrog') {
            steps {
                sh 'curl -uadmin:cmVmdGtuOjAxOjE3NzQ1NTQ0Njk6aExBRndubnFvV0tFNWUzNzhQU0dkWnVVaTg0 -T \
                ansible-${BUILD_NUMBER}.zip\
                "http://35.175.216.14:8081/artifactory/ansible/ansible-${BUILD_NUMBER}.zip"'
            }
        }
    }

}