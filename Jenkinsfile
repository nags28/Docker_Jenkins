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

def runApp(containerName, tag, dockerHubUser, httpPort){
    sh "docker run -d --rm -p 8080:80 --name $containerName $containerName:$tag"
    echo "Application started"
}

pipeline {
    agent any

    stages {
        stage('git SCM') {
            steps {
                git branch: 'feature_restructure_version3', credentialsId: '040efd0c-d708-4a87-bf3c-e00f4cb91d31', url: 'https://adept-gitsource.sonata-software.com/digital-persona/profile-portal-ui.git'
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

