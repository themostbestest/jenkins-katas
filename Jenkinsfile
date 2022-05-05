pipeline {
    agent any
    stages {
        stage('Parallel stuff') {
            parallel {
                stage('say hello') {
                    steps {
                        echo "Hello world"
                    }
                }

                stage('build app') {
                    agent {
                        docker {
                            image 'gradle:jdk11'
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
