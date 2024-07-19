pipeline{
   agent{
     label 'spc'
   }
   parameters{
      choice(name:'MAVEN',choices:['package','clean package','clean install'],description:'pick one')
   }
   tools{
     maven "MAVEN_3.9.8"
   }
   stages{
      stage('git'){
         steps{
            git branch:'main',
                url: 'https://github.com/spring-projects/spring-petclinic.git'
         }
      }
      // stage('sonar analysis'){
      //  steps{
      //    withSonarQubeEnv(credentialsId:'SONARQUBE',installationName:'SONAR_CLOUD') { // You can override the credential to be used, If you have configured more than one global server connection, you can specify the corresponding SonarQube installation name configured in Jenkins
      // sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.11.0.3922:sonar -D sonar.organization=siadevops -D sonar.projectKey=56b31a9dafb3da3d26322d9bf80735a57fc4c2d5'
      //   }
      //  }
      // }
      stage('build'){
       steps{
          sh "mvn ${params.MAVEN}"
          junit testResults: '**/surefire-reports/*.xml'
          archiveArtifacts artifacts: '**/target/spring-petclinic-*.jar'
       }
     }
      // stage('QualityGate'){
      //    steps{
      //       timeout(time:1, unit:'HOURS') {
      //               // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
      //               // true = set pipeline to UNSTABLE, false = don't
      //       waitForQualityGate abortPipeline: true
      //       }
      //    }
      // }
    
   }
}