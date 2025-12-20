pipeline {
  agent any

  environment {
    // CHANGE THIS LINE to YOUR Docker Hub username:
    DOCKERHUB_REPO = "YOUR_DOCKERHUB_USERNAME/jenkins-pipeline-project"
    IMAGE_TAG = "${env.BUILD_NUMBER}"
  }

  stages {
    stage('Checkout') {
      steps { checkout scm }
    }

    stage('Docker Build') {
      steps {
        sh '''
          docker --version
          docker build -t ${DOCKERHUB_REPO}:${IMAGE_TAG} .
        '''
      }
    }

    stage('Docker Login') {
      steps {
        withCredentials([usernamePassword(
          credentialsId: 'dockerhub-creds',
          usernameVariable: 'DH_USER',
          passwordVariable: 'DH_PASS'
        )]) {
          sh 'echo "$DH_PASS" | docker login -u "$DH_USER" --password-stdin'
        }
      }
    }

    stage('Docker Push') {
      steps {
        sh '''
          docker push ${DOCKERHUB_REPO}:${IMAGE_TAG}
          docker tag ${DOCKERHUB_REPO}:${IMAGE_TAG} ${DOCKERHUB_REPO}:latest
          docker push ${DOCKERHUB_REPO}:latest
        '''
      }
    }
  }

  post {
    always {
      sh 'docker logout || true'
      cleanWs()
    }
  }
}

