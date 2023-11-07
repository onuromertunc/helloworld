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
    stage('Push image') {
    docker.withRegistry('192.168.1.183:6161', 'dockerhub') {
        app.push("${env.BUILD_NUMBER}")
        app.push("latest")
    }
}
  
  }
}