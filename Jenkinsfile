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
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin 192.168.1.183:6161'
      }
    }
    
     stage('tag') {
      steps {
        sh 'docker tag onuromertunc/helloworld 192.168.1.183:6161/onuromertunc/helloworld:latest'
      }
    }

    stage('Push') {
      steps {
        sh 'docker push 192.168.1.183:6161/dockerprivate:latest'
      }
    }
  
  }
}