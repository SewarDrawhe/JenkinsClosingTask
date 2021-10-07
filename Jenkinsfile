pipeline {
    agent {label 'slave'}


    stages {
        stage('Cloning Git') {
            steps {
                git 'https://github.com/SewarDrawhe/JenkinsClosingTask.git'
            }
        }
        
        stage('Build') {
            steps {
                dir('./') {
                    sh "chmod +x gradlew"
                    sh './gradlew build'
                }
                
            }
        }
         stage('run the app') {
            steps {
                sh 'jps | grep demo-0.0.1 | awk \'{print "kill -9 "$1}\' | bash -x'
                
            }
            
             post {
                //in case of success : send a success message to my channel in slack
                success {
                        slackSend channel: '#fursa', color: '#008000', message: 'Successfully built', tokenCredentialId: 'slack'}
                //in case of failure : send a failure message to my channel in slack
                failure {
                        slackSend channel: '#fursa', color: '#FF0000', message: 'Failed build', tokenCredentialId: 'slack'}
            }
            
        
        
}
}
}
