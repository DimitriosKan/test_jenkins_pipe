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
					sh 'pwd'
					sh "echo ${PEM}"
					sh """
						ssh -T -i ${PEM} -o StrictHostKeyChecking=no ec2-user@ec2-34-244-126-165.eu-west-1.compute.amazonaws.com"
						pwd
					"""
					sh 'pwd'
					sh "scp -i ${PEM} -o StrictHostKeyChecking=no /home/ec2-user/push.sh ec2-user@ec2-34-244-126-165.eu-west-1.compute.amazonaws.com:/home/ec2-user/"
				}
			}
		}
	}
}
