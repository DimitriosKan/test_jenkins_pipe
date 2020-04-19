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
					sshUserPrivateKey (credentials: 'thenexus', keyFileVariable: 'PEM')
				]) {
					"$PEM"
					sh "thing ${PEM}"
				}
			}
		}
	}
}
