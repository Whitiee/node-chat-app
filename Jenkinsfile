pipeline {
	agent any
	tools {
		nodejs "node"
	}

    stages {
	     stage('Build') {
            steps {
                echo 'Build..'
		        sh 'npm install'
		    script { 
			    currentBuild.result='UNSTABLE'
		    }
            }
	  }
        stage('Test') {
            steps {
                echo 'Testing..'
		    script { 
			    if (currentBuild.result == 'UNSTABLE')
			    	error("Break")
		    }
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
