pipeline {
   agent { label 'JDK-8' }
   options {
    timeout(time: 30, unit: 'MINUTES')
   }
   triggers { pollSCM ('H/30 * * * *') }
   
  

   tools {
       
       jdk 'JDK_8'

   }
   
   

   stages {
      stage('git') {
         steps {
            git branch: 'master',
                url: 'https://github.com/dinup-test/jenkins1.git'
         }
      }
      
        stage(Sonaranalysis) {
            steps {
                
  
    
      sh 'mvn clean package sonar:sonar -Dsonar.organization=devopscharlie -Dsonar.token=e7b624387f9cd0cb2131066c6dd9d473023cc02d -Dsonar.projectKey=Test'

    }
            }

        }
        
      stage('reporting') {
        steps {       
             junit testResults: '**/surefire-reports/TEST-*.xml'
             
        }
      }
   }

   post {

      
      success {
         mail subject: "${JOB_NAME} build status",
              body : "you build is efective \n ${BUILD_URL}",
              to: "qt@all.com"
      }

      failure {
         mail subject: "${JOB_NAME} build status",
              body : "you build is defective \n ${BUILD_URL}",
              to: "qt@all.com"
      }
    

}

    

}
