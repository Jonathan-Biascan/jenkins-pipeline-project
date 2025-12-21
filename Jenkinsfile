pipeline {
  agent any
  agent any

  environment {
    VENV = ".venv"
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
        sh 'ls -la'
      }
    }

    stage('Build (Install Dependencies)') {
      steps {
        sh '''
          python3 -m venv ${VENV}
          . ${VENV}/bin/activate
          pip install --upgrade pip
          pip install -r requirements.txt
        '''
      }
    }

    stage('Docker Login') {
      steps {
        sh '''
          . ${VENV}/bin/activate

          # If pytest is installed, use it; otherwise run unittest
          if python -c "import pytest" >/dev/null 2>&1; then
            pytest -q
          else
            python -m unittest -v
          fi
        '''
      }
    }

    stage('Deploy (Demo)') {
      steps {
        sh '''
          . ${VENV}/bin/activate
          echo "Demo deploy: start app briefly to prove it runs"
          (python app.py > app.log 2>&1 &)
          sleep 2
          echo "Process check:"
          ps aux | grep -E "python.*app.py" | grep -v grep || true
          echo "Log preview:"
          tail -n 30 app.log || true
          echo "Stopping app..."
          pkill -f "python app.py" || true
        '''
      }
    }
  }

  post {
    always {
      cleanWs()
    }
  }
}

