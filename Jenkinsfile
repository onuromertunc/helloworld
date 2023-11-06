pipeline {
	agent any
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
  stages {
  	
    stage('Docker Build') {
    	agent any
      steps {
      	sh 'docker build -t onuromertunc/helloworld:latest .'
      }
    }

    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push onuromertunc/helloworld:latest'
      }
    }
  
  }
}