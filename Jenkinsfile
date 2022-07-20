pipeline {
  agent any
    
  tools {nodejs "node"}
    
  stages {
             
    stage('Build') {
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
  }
  
  post {    
    always {
      emailext body: "${currentBuild.currentResult}: Job ${env.JOB_NAME}\nMore Info can be found here: ${env.BUILD_URL}", 
               recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], 
               subject:  "jenkins build:${currentBuild.currentResult}: ${env.JOB_NAME}",
               attachLog: true
      }
    }
  }
