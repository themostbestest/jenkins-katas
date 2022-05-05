// Create an empty map that will contain our stages
def mapOfStages = [:]

// Manually add the "hello" stage
mapOfStages["hello"] = {
    stage ('Say hello') {
        echo "hello"
    }
}

// Use a foreach loop to create one stage per entry in the dockerImages list
def dockerImages = ["gradle:jdk8","gradle:6-jdk11","gradle:jdk13"]
dockerImages.each {
    // "${it}" is the iterator pointing to the current entry. So we dynamically insert, for instance, "gradle"jdk8" in all the places in the stage where it makes sense
    mapOfStages["${it}"] = { 
        docker.image("${it}").inside {
            stage("${it}") {
                lock ('checkoutLock') { // We use a "lock" built into Jenkins, to make sure only one parallel step is doing this at a time. Checking out code in parallel in scripted pipelines is not completely thread-safe...
                    git 'https://github.com/praqma-training/jenkins-katas.git'
                }
                sh 'ci/build-app.sh'
                archiveArtifacts 'app/build/libs/'
            }
        }
    }
}

// This is where we execute the map of stages that we have built
node { 
    stage('Parallel stuff') {
        parallel mapOfStages
    }
}