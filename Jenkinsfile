pipeline {
   agent { label 'JDK-8' }
   options {
    timeout(time: 30, unit: 'MINUTES')
   }
   triggers { pollSCM ('H/30 * * * *') }
   
  

   tools {
       maven 'MAVEN_LATEST'
       jdk 'JDK_8'

   }
   parameters {
        choice(name: 'MAVEN_GOAL', choices: ['package', 'clean package', 'install', 'clean install'], description: 'Maven Goal')
    }
   

   stages {
      stage('git') {
         steps {
            git branch: 'master',
                url: 'https://github.com/dinup-test/jenkins1.git'
         }
      }
        
      stage('build') {
         steps {
            sh script: "mvn ${params.MAVEN_GOAL}"
         }
      }

      stage('reporting') {
        steps {       
             junit testResults: '**/surefire-reports/TEST-*.xml'
             archiveArtifacts artifacts: '**/target/gameoflife.war'
        }
      }
   }

   post {

      
      success {
          mail subject : 'Build success'
               body: 'Buils is effective'
               to: 'all@all.com'
      }

      failure { 
         mail subject : 'Build success'
               body: 'Buils is dffective'
               to: 'all@all.com'
      }

}
    

}
