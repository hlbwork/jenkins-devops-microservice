pipeline {
	agent any
	// agent {
	// 	docker{
	// 		image 'maven:3.6.3'
	// 		// image: 'node:13.8'
	// 	}
	// }

	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage('Build'){
			steps {
				sh "mvn --version"
				sh "docker --version"
				echo 'Declarative - Builds'	
				echo '$env.BUILD_NUMBER'	
				echo '$env.BUILD_ID'
				echo '$env.JOB_NAME'	
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
