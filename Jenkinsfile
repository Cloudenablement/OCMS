pipeline {
   agent any
   stages {
       stage('Prerequisites') {
           environment {
               SAMPLE = 'sample variable'
           }
           steps
           {
                   winRMClient credentialsId: 'llg00fbd.uk.oracle.com_kurravi_1540976452', hostName: 'llg00fbd.uk.oracle.com', winRMOperations: [invokeCommand('mkdir C:\\Monal')]
           }
       }
   }
   post {
       always {
           echo 'This will always run'
       }
       success {
           echo 'This will run only if successful'
       }
       failure {
           echo 'This will run only if failed'
       }
       unstable {
           echo 'This will run only if the run was marked as unstable'
       }
       changed {
           echo 'This will run only if the state of the Pipeline has changed'
           echo 'For example, if the Pipeline was previously failing but is now successful'
       }
   }
}
