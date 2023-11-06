pipeline {
	agent any
  stages {
  	
    stage('Docker Build') {
    	agent any
      steps {
      	sh 'docker build -t onuromertunc/helloworld:latest .'
      }
    }

    stage('Docker Push') {
    	agent any
      steps {
      	withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials')]) {
        	sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh 'docker push onuromertunc/helloworld:latest'
        }
      }
    }
  }
}