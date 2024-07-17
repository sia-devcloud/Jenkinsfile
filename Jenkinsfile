pipeline {
 agent {
  label "spc"
 }
 tools {
  dotnetsdk 'SDK-8'
 }
 stages {
  stage ("Git"){
   steps {
    echo 'Cloning repository...'
    git branch: 'develop', changelog: false, poll: false, url: 'https://github.com/nopSolutions/nopCommerce.git'

   }
  }
   stage ('Build') {
    steps{
    dotnetPublish configuration: 'Release',
     outputDirectory: 'publish',
     project : 'src/Presentation/Nop.Web/Nop.Web.csproj'
    }
   }
 }
 post {
  failure {
      mail from: 'jenkins@gmail.com',
      to: 'all@gmail.com',
      subject:"Jenkins Pipeline:Build ${BUILD_ID}",
       body:"""  
        Build of ${JOB_BASE_NAME} with BuildId= ${BUILD_ID} hsa failed
          """
      }
  success {
        mail from: 'jenkins@gmail.com',
        to: 'all@gmail.com',
        subject:"Jenkins Pipeline:Build ${BUILD_ID}",
        body:"""
          Build of ${JOB_BASE_NAME} with BuildId= ${BUILD_ID} hsa been succeeded
          """
        }
      }
  
  }