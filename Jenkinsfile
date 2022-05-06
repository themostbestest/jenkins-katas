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

      }
    }

    stage('Component test') {
      agent {
        docker {
          image 'gradle:6-jdk11'
        }
      }
      when {
        beforeAgent true
        anyOf {
          branch pattern: "^(?!dev)\\S+$", comparator: "REGEXP"
          changeRequest()
        }
      }
      steps {
        echo 'Component test'
        sh 'ci/component-test.sh'
      }
    }

    stage('Deploy') {
      when {
        branch 'master'
      }
      steps {
        echo 'Deploying'
      }
    }

  }
}