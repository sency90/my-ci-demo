pipeline {
  agent any
  options { timestamps() }
  stages {
    stage('Checkout') {
      steps {
        git url: 'https://github.com/sency90/my-ci-demo.git', branch: 'main'
      }
    }
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
        sh 'ctest --test-dir build --output-on-failure'
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

