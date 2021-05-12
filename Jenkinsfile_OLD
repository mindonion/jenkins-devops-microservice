
//SCRIPTED (Old way)


//DECLARATIVE
pipeline {
	agent any
	//agent {docker { image 'maven:3.8.1'} }
	stages {
		stage('Build') {
			steps {
				//sh "mvn --version"
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD NUMBER - $env.$BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_TAG"
			}
		}
		stage('Test') {
			steps {
				echo "Test"
			}
		}
		stage('Integration Test') {
			steps {
				echo "Integration Test"
			}
		}
	}

	post {
		always {
			echo 'I am awesome, I run always'
		}
		success {
			echo 'I run when you are successful'
		}
		failure {
			echo 'I run when this fails'
		}
	}
}