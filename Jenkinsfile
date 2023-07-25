pipeline {
   agent { label 'JDK-8' }
   options {
    timeout(time: 30, unit: 'MINUTES')
   }
   triggers {
    pollSCM'(* * * * *)'
   }
  

   tools {
       maven 'MAVEN_LATEST'
       jdk 'JDK_8'

   }


   stages {
      stage('git') {
         step {
            git branch: Master
                url: https://github.com/dinup-test/jenkins1.git
         }
      }
        
      stage('build') {
         step {
            sh script 'mvn clean install'
         }
      }

      stage('reporting') {
        step {
            archiveArtifacts artifacts 'target/*.jar'
            junit testResults '**/target/surefire-reports/TEST-*.xml'
        }
      }
   }
}
    

