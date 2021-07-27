pipeline {
  agent {
    docker {
      image 'maven:3-alpine'
      args '-v /root/.m2:/root/.m2'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'mvn -B -Denforcer.skip=true -DskipTests clean package'
      }
    }

    stage('Deliver') {
      parallel {
        stage('Deliver') {
          steps {
            sh './jenkins/scripts/deliver.sh'
          }
        }

        stage('Test') {
          steps {
            junit 'target/surefire-reports/*.xml'
          }
        }

      }
    }

  }
}