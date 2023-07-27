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
      stage ('Artifactory configuration') {
            steps {
                
                rtMavenDeployer (
                    id: "GOL_DEPLOYER",
                    serverId: "JFROG_TOKEN",
                    releaseRepo: 'devops-snapshot-local',
                    snapshotRepo: 'devops-snapshot-local'
                )

               //(this for downloading things from central repo or internet) rtMavenResolver (
                  //  id: "MAVEN_RESOLVER",
                  //  serverId: "ARTIFACTORY_SERVER",
                  //  releaseRepo: ARTIFACTORY_VIRTUAL_RELEASE_REPO,
                  //  snapshotRepo: ARTIFACTORY_VIRTUAL_SNAPSHOT_REPO
                
            }
        }

        stage ('Exec Maven') {
            steps {
                rtMavenRun (
                    tool: MAVEN_LATEST, // Tool name from Jenkins configuration
                    pom: 'pom.xml',
                    
                    deployerId: "GOL_DEPLOYER",
                    buildName: "${JOB_NAME}",
                    buildNumber: "${BUILD_ID}"
                    
                )
            }
        }

        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "JFROG_TOKEN"
                )
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
