pipeline {
  agent any
  stages {
    stage('Parallel stuff') {
      parallel {
        stage('say hello') {
          steps {
            echo 'Hello world'
          }
        }

        stage('build app default') {
          agent {
            docker {
              image 'gradle:6-jdk11'
            }

          }
          steps {
            sh 'ci/build-app.sh'
            archiveArtifacts 'app/build/libs/'
          }
        }

        stage('build app jdk8') {
          agent {
            docker {
              image 'gradle:jdk8'
            }

          }
          steps {
            sh 'ci/build-app.sh'
            archiveArtifacts 'app/build/libs/'
          }
        }

        stage('build app jdk13') {
          agent {
            docker {
              image 'gradle:jdk13'
            }

          }
          steps {
            sh 'ci/build-app.sh'
            archiveArtifacts 'app/build/libs/'
          }
        }

      }
    }

  }
}