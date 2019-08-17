node {
    
	

    env.AWS_ECR_LOGIN=true
    def newApp
    def registry = 'sharmashantanu07/first-docker'
    def registryCredential = 'dockerhub'
	
	stage('Git') {
		git 'https://github.com/tavisca-ssharma/node-todo-frontend-master'
	}
	stage('Build') {
		powershell '''npm install'''
	}
	stage('Test') {
		powershell '''npm test'''
	}
	stage('Building image') {
        docker.withRegistry( 'https://' + registry, registryCredential ) {
		    def buildName = registry + ":$BUILD_NUMBER"
			newApp = docker.build buildName
			newApp.push()
        }
	}
	stage('Registring image') {
        docker.withRegistry( 'https://' + registry, registryCredential ) {
    		newApp.push 'latest2'
        }
	}
    stage('Removing image') {
        sh "docker rmi $registry:$BUILD_NUMBER"
        sh "docker rmi $registry:latest"
    }
    
}
