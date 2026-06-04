pipeline {
  agent {
    dockerfile {
      filename 'Dockerfile'
      label 'docker-agent'
      args '--rm'
    }
  }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Build and Test') {
      steps {
        sh 'mvn -B clean test'
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
