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
				//bat 'wmic computersystem get name'
			}
		}
		stage('Execute command on host') {
			steps {
				withCredentials([
					sshUserPrivateKey (credentialsId: 'thenexus', keyFileVariable: 'PEM')
				]) {
					sh "echo ${PEM}"
					sh "ssh -T -i ${PEM} ec2-user@ec2-63-35-228-112.eu-west-1.compute.amazonaws.com"
					sh 'pwd'
					//scp -i $PEM push.sh ec2-user@ec2-63-35-228-112.eu-west-1.compute.amazonaws.com:/home/ec2-user/downloads
				}
			}
		}
	}
}
