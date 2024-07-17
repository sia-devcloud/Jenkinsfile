pipeline {
 agent {
  label "spc"
 }
 tools{
    maven "MAVEN_3.9.8"
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
 parameters{
    choice( name:'maven_goal',choices: ['package','clean package','clean install'],description: 'pick one')
 }
 stages {
  stage ("Git"){
   steps {
    echo 'Cloning repository...'
    git branch: 'main',
        url: 'https://github.com/spring-projects/spring-petclinic.git'

   }
  }
  stage ('Build') {
    steps{
    mail bcc: '', body: 'build started', cc: '', from: '', replyTo: '', subject: 'build', to: 'all@gmail.io'
  sh "mvn ${params.maven_goal}"
  archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
  junit testResults: '**/surefire-reports/*.xml'
  mail bcc: '', body: 'build completed', cc: '', from: '', replyTo: '', subject: 'build', to: 'all@gmail.io'
  }
  }
 }
}