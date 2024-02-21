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
		stage('Checkout'){
			steps {
				sh "mvn --version"
				sh "docker --version"
				echo "Declarative - Builds"
				echo "$env.BUILD_NUMBER"	
				echo "$env.BUILD_ID"
				echo "$env.JOB_NAME"	
			}	
		}

		stage ('Compile') {
			steps {
				sh "mvn clean compile"
			}	
		}
		// stage('Test'){
		// 	steps {
		// 		sh "mvn test"
		// 	}	
		// }

		// stage('Integration Test'){
		// 	steps {
		// 		sh "mvn failsafe:integration-test failsafe:verify"
		// 	}	
		// }

		stage ('Build Docer image') {
			steps {
				script {
					dockerImage = docker.build("in28min/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}

		stage ('Package') {
			steps {
				sh "mvn package -DskipTests"
			}
		}

		stage ('Push Docker image') {
			steps {
				script{
					docker.withRegistry('','dockerhub'){ // this is allowing jenkins to user our dockerhub credential we stored as as 'dockerhub'
						dockerImage.push();
						dockerImage.push('latest');
					}
				}
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
