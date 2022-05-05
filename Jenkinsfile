node { 
    stage('Parallel stuff') {
        parallel (
            "Say hello" : {
                stage ('Say hello') {
                    echo "hello"
                }
            },
            "build app" : {
                docker.image('gradle:jdk11').inside {
                    stage('Test') {
                        git 'https://github.com/praqma-training/jenkins-katas.git'
                        sh 'ci/build-app.sh'
                        archiveArtifacts 'app/build/libs/'
                    }
                }
            }
        )
    }
}
