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
    }
}

