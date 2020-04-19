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
				bat 'wmic computersystem get name'
			}
		}
		stage('Execute command on host') {
			steps {
				withCredentials([
					sshUserPrivateKey (credentialsId: 'thenexus', keyFileVariable: 'PEM')
				]) {
					bat 'echo %PEM%'
					bat 'scp -i %PEM% push.sh ec2-user@ec2-63-35-228-112.eu-west-1.compute.amazonaws.com'
					//powershell "ssh -i ${PEM} ec2-user@ec2-63-35-228-112.eu-west-1.compute.amazonaws.com"
				}
			}
		}
	}
}
