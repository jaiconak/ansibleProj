pipeline {
    agent any

    stages {
        
        stage ('Zip File') {
            steps {
                sh 'zip -r ansible-${BUILD_NUMBER}.zip * --exclude=Jenkinsfile'
                sh 'ls -l'
                sh 'echo "testing"'
            }
        }

        stage ('Upload to JFrog') {
            steps {
                sh 'curl -uadmin:cmVmdGtuOjAxOjE3NzQ1NzM1NDM6UGVQRVpRMzFmOUczNDFTR042VHB3NFBTTHox -T <PATH_TO_FILE> "http://18.215.124.40:8081/artifactory/ansible/<TARGET_FILE_PATH>"'
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