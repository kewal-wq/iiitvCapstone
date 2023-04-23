pipeline {
    agent any
    environment {
	docker_cred = credentials("22a2c9f6-8559-4d8f-ab2e-3b07fcabed00")
    }
    stages {
	stage('Login to dockerhub') {
	   steps {
		script {
		    sh "docker login -u ${docker_cred_USR} -p ${docker_cred_PSW}"
		}
	}	
     }
	stage('Removing container') {
            steps {
                script {
		    try {
			sh "docker rm -f master_container"
		   } catch (e) {
			sh 'echo "Container does not exist"'	
		}
                }
        }       
      }
        stage('Building Website') {
            steps {
                sh 'docker build . -t master_image'
            }
       }

       stage('Testing Website') {
            steps {
                sh 'echo "Testing Website"'
            }
       }

       stage('Push to Production') {
            steps {
                sh 'docker run -it -p 82:80 -d --name master_container master_image'
            }
       }
    }
}
