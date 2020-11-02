pipeline {
  agent {
        kubernetes {
          yamlFile 'pod.yaml'
        }
  }
  options { 
    skipDefaultCheckout false
  }
  stages {
    stage('x64') {
      steps {
          container("gcc8-x64") {
            sh "pwd"
            sh "ls" 
            sh 'conan install . --install-folder=tmp --profile profiles/x86_64'
            sh "conan build . --build-folder=tmp"
          }
      }
    }
    stage('armv7') {
      steps {
          container("gcc8-armv7") {
            sh "pwd" 
            sh 'ls /homme/conan/.conan'
            sh 'conan install . --install-folder=tmp --profile profiles/amrv7'
            sh "conan build . --build-folder=tmp"
          }
      }
    }
  }
}