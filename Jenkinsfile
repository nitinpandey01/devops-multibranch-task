pipeline {
  agent any
    
  tools {nodejs "node"}
    
  stages {
             
    stage('Install') {
      steps {
        sh 'npm install'
      } 
    }

    stage('Lint') {
      steps {
        sh 'npm run lint'
      }
    }  
                
    stage('Test') {
      steps {
        sh 'npm test'
      }
    }
    stage('Build') {
    steps{
      sh 'npm run build'
    }
  }
  
  post {    
    always {
      emailext body: "${currentBuild.currentResult}: Job ${env.JOB_NAME}\nMore Info can be found here: ${env.BUILD_URL}", 
               recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], 
               subject:  "jenkins build:${currentBuild.currentResult}: ${env.JOB_NAME}",
               attachLog: false
      }
    }
  }
