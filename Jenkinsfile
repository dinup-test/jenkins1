pipeline {
   agent { label 'JDK-17' }
   options {
    timeout(time: 30, unit: 'MINUTES')
   }
   triggers {
    pollSCM'(* * * * *)'
   }
  

   tools {
       maven 'apache-maven-3.9.3'
       jdk 'jdk_8'

   }


   stages {
      stage('git')
         steps {
            git branch: Master
                url: https://github.com/dinup-test/jenkins1.git
         }
        
      stage('build')
         step {
            sh script 'mvn clean install'
         }

      stage('reporting')
        step {
            archiveArtifacts artifacts 'target/*.jar'
            junit testResults '**/target/surefire-reports/TEST-*.xml'
        }
   }
}
    

