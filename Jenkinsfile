pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        checkout scm 
      }
    }
    stage('Build and Test') {
      steps {
        script {
          sh 'docker build -t jenkins-multibranch-demo .'
          sh 'docker run --rm -v "$PWD":/workspace -w /workspace jenkins-multibranch-demo mvn -B clean test'
        }
      } 
      post {
        always {
          junit 'target/surefire-reports/*.xml'
          archiveArtifacts artifacts: 'target/surefire-reports/*.xml', onlyIfSuccessful: false
        }
      }
    }
  }
}
