pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        echo 'Build: installing dependencies'
        sh 'python3 --version'
        sh 'pip3 install -r requirements.txt'
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
