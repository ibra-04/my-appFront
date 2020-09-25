node {
    def newApp
    def registry = 'brahim04/frontd-app'
    def registryCredential = 'dockerhub'
	
	stage('Git') {
		git 'https://github.com/ibra-04/my-appFront.git'
	}
	stage('Build') {
		sh 'npm install'
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