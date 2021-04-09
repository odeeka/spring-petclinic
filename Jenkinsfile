pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/odeeka/spring-petclinic.git'                
            }
        }
        stage('Build') {
            steps {
                sh './mvnw clean package'
                //sh 'true' //true
            }
            
            post {
                always {
                    emailext to: "test@jenkins", attachLog: true, body: 'Please go to ${BUILD_URL} and verify the build', compressLog: true, recipientProviders: [upstreamDevelopers(), requestor()], subject: "Job \'${JOB_NAME}\' (build ${BUILD_NUMBER}) ${currentBuild.result}"
                }
            }         

        }
    }
}
