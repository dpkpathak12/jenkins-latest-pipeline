pipeline {
	//agent any
	agent {docker {image 'maven:3.6'} }
	agent {docker {image 'nodejs:10'}}
		stages {
			stage ('checkout') {
				steps {
					sh 'mvn --version'
					sh 'node --version'
				echo "checkout stage is completed"
			}
			}
			stage ('test') {
				steps {
				echo "test stage is completed"
			}
			}
			stage ('deployment') {
				steps {
				echo "deployment stage is completed"
			}
			}
			stage ('staging') {
				steps {
					echo "staging is completed"
				}

			}
			stage ('deploy') {
				steps{
					echo "deploy stage completed"
				}
				
			}

		}

}

		
