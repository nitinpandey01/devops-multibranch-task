pipeline {
  agent any
    
  tools {nodejs "node"}
    
  stages {
             
    stage('Build') {
      steps {
        bat 'npm install'
      }
    }

    stage('Lint') {
      steps {
        bat 'npm run lint'
      }
    }  
                
    stage('Test') {
      steps {
        bat 'npm test'
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
