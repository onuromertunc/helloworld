pipeline {
	agent any
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
  stages {
  	
    stage('Docker Build') {
    	agent any
      steps {
      	sh 'docker build -t helloworld:latest .'
      }
    }

    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin 192.168.1.183:6161'
      }
    }
    
     stage('tag') {
      steps {
        sh 'docker tag helloworld 192.168.1.183:6161/helloworld:latest'
      }
    }

    stage('Push') {
      steps {
        sh 'docker push 192.168.1.183:6161/helloworld:latest'
      }
    }

     stage('Deploy to k8s'){
            steps{
                script{
                    kubernetesDeploy (configs: 'deployment.yaml',kubeconfigId: 'k8sconfigpwd')
                }
            }
        }
      }
    }
  
  
