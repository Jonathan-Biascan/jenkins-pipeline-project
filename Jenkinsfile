pipeline {
  agent {
    docker { image 'python:3.12-slim' }
  }

  stages {
    stage('Build') {
      steps {
        echo 'Build: installing dependencies'
        sh 'python --version'
        sh 'pip install -r requirements.txt'
      }
    }

    stage('Test') {
      steps {
        echo 'Test: running pytest'
        sh 'pytest -q'
      }
    }

    stage('Deploy') {
      steps {
        echo 'Deploy: simulated deploy step'
        sh 'echo "Deploy completed (simulation)."'
      }
    }
  }
}
