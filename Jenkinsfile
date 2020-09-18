def CONTAINER_NAME="ui-api"
def CONTAINER_TAG="latest"


def imagePrune(containerName){
    try {
        sh "docker image prune -f"
        sh "docker stop $containerName"
    } catch(error){}
}

def imageBuild(containerName, tag){
    sh "docker build -t $containerName:$tag  -t $containerName --pull --no-cache ."
    echo "Image build complete"
}

pipeline {
    agent any

    stages {
        stage('git SCM') {
            steps {
                git branch: 'master', url: ''
            }
        }
	stage("Image Prune"){
       steps{
	   imagePrune(CONTAINER_NAME)
		}
	}
	
	    stage('Image Build'){
        steps{
		imageBuild(CONTAINER_NAME, CONTAINER_TAG)
		}
	}
}
}

