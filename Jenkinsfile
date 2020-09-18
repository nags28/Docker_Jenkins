def CONTAINER_NAME="ui-api-2"
def CONTAINER_TAG="latest"


def imagePrune(containerName){
    try {
        sh "docker image prune -f"
        sh "docker stop ui-api"
    } catch(error){}
}

def imageBuild(containerName, tag){
    sh "docker build -t $containerName:$tag  -t $containerName --pull --no-cache ."
    echo "Image build complete"
}

def runApp(containerName, tag){
    sh "docker run -d --rm -p 9000:80 --name $containerName $containerName:$tag"
    echo "Application started"
}

pipeline {
    agent any

    stages {
        stage('git SCM') {
            steps {
                git branch: 'master', url: 'https://github.com/nags28/demo_docker_jenkins.git'
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
	    
	
    stage('Run App'){
	    steps{
	    runApp(CONTAINER_NAME, CONTAINER_TAG)
    }
    }

}
}

