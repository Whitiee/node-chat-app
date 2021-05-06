	pipeline {
	agent any
	tools {
		nodejs "node"
	}
    stages {
	stage('Install dependencies') {
            steps {
                echo 'Installing dependencies..'
		        sh 'npm install'
		    	sh 'apt install git -y'
            }
	  }
	  
	stage('Build') {
            steps {
                echo 'Building..'
		    try {
                	sh 'git clone --no-checkout https://github.com/Whitiee/node-chat-app.git'
		    }
		    catch (exc) {
			sh 'git init && git pull'
		    }
		        sh 'npm build'
            }
        }   
	  
        stage('Test') {
          when {
            expression { currentBuild.result == 'SUCCESS'}
          }
            steps {
                echo 'Testing..'
		        sh 'npm run test'
            }
        } 
    }
    post {
        always {
            echo 'I have finished'
        }
        success {
            echo 'I succeeded!'
        }
        failure {
            echo 'I failed :('
            emailext attachLog: true, 
            	     body: "Something is wrong with ${env.BUILD_URL}",
            	     subject: "Failed test Pipeline: ${currentBuild.fullDisplayName}",
            	     to: 'juliafajer69@gmail.com'
        }
    }
}
