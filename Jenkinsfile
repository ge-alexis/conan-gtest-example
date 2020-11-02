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
            sh 'conan install . --install-folder=tmp --profile profiles/x86_64 --build=missing'
            sh "conan build . --build-folder=tmp"
            sh 'ls /home/conan/.conan'
          }
      }
    }
    stage('armv7') {
      steps {
          container("gcc8-armv7") {
            sh "pwd" 
            sh 'ls /home/conan/.conan'
            sh 'sudo apt-get -y install gcc-arm*'
            sh 'conan install . --install-folder=tmp --profile profiles/armv7 --build=missing'
            sh "conan build . --build-folder=tmp"
          }
      }
    }
  }
}