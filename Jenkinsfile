pipeline {
   agent { label 'JDK-8' }
   options {
    timeout(time: 30, unit: 'MINUTES')
   }
   triggers {
    pollSCM('* * * * *')
   }
  

   tools {
       maven 'MAVEN_LATEST'
       jdk 'JDK_8'

   }
   
   parameters {
      choice(name: 'GOAL', CHOICES: ['clean', 'clean install', 'clean package'], discription: 'choices for Goal')
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
            sh script: 'mvn ${param.GOAL}'
         }
      }

      stage('reporting') {
        steps {
            archiveArtifacts artifacts: '**/target/gameoflife.war'
            junit testResults: '**/target/surefire-reports/TEST-*.xml'
        }
      }
   }
}
    

