
//SCRIPTED (Old way)


//DECLARATIVE
pipeline {
	agent any
	//agent {docker { image 'maven:3.8.1'} }
    environment {
        dockerHome = tool 'myDocker'
        mavenHome = tool 'myMaven'
        PATH = "$dockerHOME/bin:$mavenHome/bin:$PATH"
    }

	stages {
		stage('Checkout') {
			steps {
				sh "mvn --version"
                sh "docker version"
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD NUMBER - $env.$BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_TAG"
			}
		}
		stage('Compile') {
			steps {
				sh "mvn clean compile"
			}
		}
		stage('Test') {
			steps {
				sh "mvn test"
			}
		}
		stage('Integration Test') {
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
		stage('Package') {
			steps {
				sh "mvn package -DskipTests"
			}
		}

		stage('Build Docker Image') {
			steps {
				//"docker build -t in28min/currency-exchange-devops:$env.BUILD_TAG"
				script {
					docker build("dockerlab001/private-test-repo:$env.BUILD_TAG")
				}
			}

		}

		stage('Push Docker Image') {
			steps {
				script {
					docker.withRegistry('', 'bb9a874f-44d1-43b7-b31f-12072eb6d5cb') {
						dockerImage.push();
						dockerImage.push('latest');
					}
				}
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