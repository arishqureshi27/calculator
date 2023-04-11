pipeline {
  agent any
  tools{
  nodejs "nodejs"
  }
  stages {
    stage('Checkout') {
      steps {
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/arishqureshi27/calculator.git']]])
      }
    }
    stage('Install dependencies') {
      steps {
        nodejs('node') {
          sh 'npm install'
        }
      }
    }
    stage('Run tests') {
      steps {
        nodejs('node') {
          sh 'npm run test -- --watchAll=false'
        }
      }
    }
    stage('Build') {
      steps {
        nodejs('node') {
          sh 'npm run build'
        }
      }
      post {
        always {
          archiveArtifacts artifacts: 'build/**'
        }
      }
    }
  }
}
