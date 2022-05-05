node { 
    stage('Parallel stuff') {
        parallel (
            "Say hello" : {
                stage ('Say hello') {
                    echo "hello"
                }
            },
            "build app" : {
                docker.image('gradle:6-jdk11').inside {
                    stage('Test') {
                        git 'https://github.com/themostbestest/jenkins-katas.git'
                        sh 'ci/build-app.sh'
                        archiveArtifacts 'app/build/libs/'
                    }
                }
            }
        )
    }
}
