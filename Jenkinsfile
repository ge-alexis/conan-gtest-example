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
            sh "cd tmp/test/bin/ && ./GoogleTests"
            sh 'rm -rf tmp'
            sh 'ls /home/conan/.conan'
          }
      }
    }
    stage('armv7') {
      steps {
          container("gcc8-armv7") {
            sh "pwd" 
            sh 'ls -r /home/conan/.conan'
            sh 'conan install . --install-folder=tmp --profile profiles/armv7 --build=missing'
            sh "conan build . --build-folder=tmp"
          }
        /*  container("arm32v7") {
            sh "cd tmp/test/bin/ && ./GoogleTests"
          }
          */
      }
    }
    stage("windows") {
      agent {
        kubernetes {
          yamlFile 'windows-pod.yaml'
        }
      }
      steps {
        container('shell') {
          powershell 'Get-ChildItem Env: | Sort Name'
          powershell 'ls'
          powershell 'nuget'
          powershell 'msbuild -h'
        }
      }
    }
  }
}