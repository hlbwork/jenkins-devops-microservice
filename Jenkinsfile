pipeline {
	// agent any
	agent {
		docker{
			image 'maven:3.6.3'
		}
	}
	stages {
		stage('Build'){
			steps {
				sh "mvn --version"
				echo 'Declarative - Builds'	
			}	
		}
		stage('Test'){
			steps {
				echo 'Declarative - Test'	
			}	
		}
	} 
	post {
		always {
			echo 'Always'
		}
		success {
			echo 'on Success'
		}
		failure {
			echo 'Boo, broken'
		}
		changed {
			echo 'On the  build status changes ...'
		}
	}
}
