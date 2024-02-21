pipeline {
	agent any
	stages {
		stage('Build'){
			steps {
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
	}
}
