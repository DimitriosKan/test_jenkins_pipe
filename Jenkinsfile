pipeline {
	agent any

	stages {
		stage('Just a Test Stage') {
			steps {
				echo 'Test stage ...'
			}
		}
		stage('Check Param') {
			steps {
				echo 'The value of the param is $ssh_creds'
			}
		}
		stage('Execute command on host') {
			steps {
				withCredentials([
					sshUserPrivateKey (credentialsId: 'thenexus', keyFileVariable: 'PEM')
				]) {
					echo "$PEM"
					echo "%PEM%"
					"ssh -i %PEM% ec2-user@ec2-63-35-228-112.eu-west-1.compute.amazonaws.com"
					pwd
				}
			}
		}
	}
}
