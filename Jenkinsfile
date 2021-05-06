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
		        sh 'install git'
            }
	  }
	  
	stage('Build') {
            steps {
                echo 'Building..'
                	sh 'git clone https://github.com/Whitiee/node-chat-app.git'
		        sh 'npm run build'
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
