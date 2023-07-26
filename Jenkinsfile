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
         mail subject : "build status",
              body : "you build is efective",
              to: "qt@all.com"
      }

      failure {
         mail subject : "build status",
              body : "you build is defective",
              to: "qt@all.com"
      }

}
    

}
