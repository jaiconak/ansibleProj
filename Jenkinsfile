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

        stage ('PUSH FILES VIA SSH Ansible') {
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: \
                'AnsibleServer', transfers: [sshTransfer(cleanRemote: false, \
                excludes: '', execCommand: 'ls', execTimeout: 120000, flatten: false, \
                makeEmptyDirs: false, noDefaultExcludes: false, \
                patternSeparator: '[, ]+', remoteDirectory: '/home/ec2-user', \
                remoteDirectorySDF: false, removePrefix: '', \
                sourceFiles: 'ansible-${BUILD_NUMBER}.zip')], usePromotionTimestamp: false, \
                useWorkspaceInPromotion: false, verbose: false)])
            }

        }
    }

}