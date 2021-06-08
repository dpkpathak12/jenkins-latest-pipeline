pipeline {
	agent any
//agent { docker { image "maven:6.3.0"} }
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$mavenHome/bin:$PATH"
	}
	stages {

		stage ('permission') {
			steps {
				//sh "chmod 777 -R /var/jenkins_home/workspace/jenkins-devops-pipeline@tmp"
				echo "Permission checking"
			}	
		}

		stage('checkout') {
			steps {
				
				sh "docker version"
				//sh "chmod 777 -R /var/jenkins_home/workspace/jenkins-devops-pipeline@tmp/durable*"
				sh "mvn --version"
				
				echo "Build"

				echo "BUILD_ID - $env.BUILD_ID"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "$PATH - $env.PATH"
				echo "JOB_ID - $env.JOB_ID"
				echo "JOB_URL - $env.JOB_URL"
				echo "BUILD_URL - $env.BUILD_URL"
				
				echo "installation successful"
				}
		}
		stage('compile') {
				steps {

				sh "mvn clean compile"
			}
		}
		stage('test') {
			steps {
				sh "mvn test"	
					}
		}			
		stage('integration test') {
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"	
					}
		}
		stage('integration test not reopen') {
			steps {
				sh "mvn package -DskipTests"	
					}
		}
		stage('docker build') {
			steps {
				//sh "chmod 777 -R /var/jenkins_home/workspace/jenkins-devops-pipeline@tmp/durable*"
				script{
					dockerImage = docker.build("dpkp125/currency-exchange-devops:${env.BUILD_ID}")
				}
			}
		}
		stage('docker push') {
			steps {
				script {
					docker.withRegistry('', 'dockerhub') {
						dockerImage.push()
						dockerImage.push('latest')
					}
				}
			}
		}
		
	}
}
