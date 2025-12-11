pipeline {
    agent any
    environment {
        DOCKER_HUB_CREDENTIALS = credentials('docker-hub-credentials')
    }
    stages {
	stage('Clone Repository'){
            steps{
                git branch: 'main', url: 'https://github.com/pratham2441/node-js-sample.git'
            }
        }
	stage('Build Docker Image') {
	    steps {
		sh 'docker build -t node-js-sample:1.0 .'
	    }
	}
	stage('Push to Docker Hub') {
	    steps {
		sh 'docker login -u $DOCKER_HUB_CREDENTIALS_USR -p $DOCKER_HUB_CREDENTIALS_PSW'
		sh 'docker tag node-js-sample:1.0 prathamesh24/node-js-sample:1.0'
		sh 'docker push prathamesh24/node-js-sample:1.0'
	    }
	}
	stage('Deploy to kubernetes') {
	    steps {
		sh 'kubectl apply -f k8s/deployment.yaml'
	    }
	}
    }
}
