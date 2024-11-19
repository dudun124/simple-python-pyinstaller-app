node {
  stage('Build') {
    docker.image('python:2-alpine').inside {
      sh 'python -m py_compile ./sources/add2vals.py ./sources/calc.py'
    }
  }
  stage('Test') {
    docker.image('qnib/pytest').inside {
      sh 'py.test --verbose --junit-xml test-reports/results.xml ./sources/test_calc.py'
    }
    junit 'test-reports/results.xml'
  }
  stage('Manual Approval') {
    input message: 'Lanjutkan ke tahap Deploy?',
          ok: 'Proceed',
          parameters: []
  }

  stage('Deploy') { 
    docker.image('python:2-alpine').inside {
      sh '''
        echo "Starting deployment..."
        python -m http.server 8000 &
      '''
    }
    echo 'Aplikasi berjalan selama 1 menit untuk percobaan...'
    sleep(time: 60, unit: 'SECONDS') 
    sh 'pkill -f "python -m http.server" || true'
    echo 'Deployment selesai.'
  }
} 