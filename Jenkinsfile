pipeline {
  agent any
  options { timestamps() }
  stages {
    stage('Build') {
      steps {
        sh '''
          rm -rf build
          cmake -S . -B build -DCMAKE_BUILD_TYPE=Release
          cmake --build build -j
        '''
      }
    }
    stage('Test') {
      steps {
        sh 'ctest --test-dir build --output-on-failure --output-junit build/ctest-report.xml'
      }
    }
    stage('Package') {
      steps {
        sh 'tar -czf build/hello_ci.tgz -C build hello'
        archiveArtifacts artifacts: 'build/hello_ci.tgz', fingerprint: true
      }
    }
  }
  post {
    always {
      junit allowEmptyResults: true, testResults: '**/build/Testing/**/*.xml'
    }
  }
}

