pipeline {
   agent { label 'JDK-8' }
   options {
    timeout(time: 30, unit: 'MINUTES')
   }
  triggers { pollSCM ('H/30 * * * *') }
    parameters {
        choice(name: 'MAVEN_GOAL', choices: ['package', 'install', 'clean'], description: 'Maven Goal')
    }
  

   tools {
       maven 'MAVEN_LATEST'
       jdk 'JDK_8'

   }
   parameters {
      choice(name: 'GOAL', choices: ['package', 'install' 'clean'], discription: 'this for choices')

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
            sh "mvn ${params.GOAL}"
         }
      }

      stage('reporting') {
        steps {
            archiveArtifacts artifacts: '**/target/gameoflife.war'
            junit testResults: '**/target/surefire-reports/TEST-*.xml'
        }
      }
   }

   post {
      success {
         mail subject : "build status"
              body : "you build is efective"
      }

      failure {
         mail subject : "build status"
              body : "you build is defective"
      }



   }
}
    

