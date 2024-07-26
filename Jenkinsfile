pipeline{
    agent any

    stages{
        stage('zip the file'){
            steps{
                sh 'zip ansible-$BUILD_ID.zip * --exclude Jenkinsfile'
            }
        }
        stage('upload artifact to jfrog'){
            steps{
                sh 'curl -uadmin:AP5Wqb4z8e2FpTCsrqdrpHBVngW -T ansible-$BUILD_ID.zip \
                "http://52.200.226.47:8081/artifactory/ansible/ansible-$BUILD_ID.zip"'
            }
        }
        stage('upload artifact to ansible server'){
            steps{
                sshPublisher(publishers: [sshPublisherDesc(configName: 'ansible-server', \
                transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', \
                execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, \
                patternSeparator: '[, ]+', remoteDirectory: '.', remoteDirectorySDF: false, \
                removePrefix: '', sourceFiles: 'ansible-${BUILD_ID}.zip')], usePromotionTimestamp: false, \
                useWorkspaceInPromotion: false, verbose: false)])
            }
        }
    }
}

