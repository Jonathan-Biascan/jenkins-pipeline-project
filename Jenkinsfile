pipeline {
  agent {
    docker {
      image 'python:3.12-slim'
      args '-u root'
    }
  }

  environment {
    HOME = "/tmp"
    PIP_CACHE_DIR = "/tmp/pip-cache"
  }

  stages {
    stage('Build') {
      steps {
        echo 'Build: installing dependencies'
        sh 'python --version'
        sh 'python -m pip install --upgrade pip'
        sh 'python -m pip install --user -r requirements.txt'
      }
    }

    stage('Test') {
      steps {
        echo 'Test: running pytest'
        sh 'python -m pytest -q'
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
