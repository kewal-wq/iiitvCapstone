pipeline {
    agent any
    environment {
	docker_cred = credentials("726e25c0-c230-446e-ab9c-8b4c63a1f888
")
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
