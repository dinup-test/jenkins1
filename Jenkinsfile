pipeline {
   agent(JDK-8)
   options {
    timeout(time: 30, unit: 'MINUTES')
   }
   triggers {
    cron(* * * * *)
   }
   parameters {
    string(name:'PERSON', defaultvalue 'Mr jenkins',  description 'Hi, this is test run')
   }

   tools {
       maven 'apache-maven-3.9.3'
       jdk 'jdk_8'

   }


   stages {
      stage('git')
         steps {
            git branch: Main 
                url: https://github.com/wakaleo/game-of-life.git
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




   


git branch: main 
            url: https://github.com/wakaleo/game-of-life.git
        }

        stage('build')
           sh script 'mav clean install'



