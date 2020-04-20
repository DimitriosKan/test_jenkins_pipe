pipeline {
	agent any

	stages {
		stage('Just a Test Stage') {
			steps {
				echo 'Test stage ...'
			}
		}
		stage('Initial Test SSH') {
			steps {
				withCredentials([
					sshUserPrivateKey (credentialsId: 'thenexus', keyFileVariable: 'PEM')
				]) {
					sh 'pwd'
					sh "ssh -T -i ${PEM} -o StrictHostKeyChecking=no ec2-user@ec2-34-244-126-165.eu-west-1.compute.amazonaws.com pwd"
					//sh "scp -i ${PEM} -o StrictHostKeyChecking=no /home/ec2-user/push.sh ec2-user@ec2-34-244-126-165.eu-west-1.compute.amazonaws.com:/home/ec2-user/"
					sh "ssh -T -i ${PEM} -o StrictHostKeyChecking=no ec2-user@ec2-34-244-126-165.eu-west-1.compute.amazonaws.com rm /home/ec2-user/SK_Tama_Black_JPEG.jpg"
					sh "ssh -T -i ${PEM} -o StrictHostKeyChecking=no ec2-user@ec2-34-244-126-165.eu-west-1.compute.amazonaws.com aws s3 cp s3://fresh-test-bucket/SK_Tama_Black_JPEG.jpg /home/ec2-user/"
					sh "ssh -T -i ${PEM} -o StrictHostKeyChecking=no ec2-user@ec2-34-244-126-165.eu-west-1.compute.amazonaws.com ls /home/ec2-user/"
				}
			}
		}
		stage('Copy file in Slave') {
			steps {
				withCredentials([
					sshUserPrivateKey (credentialsId: 'thenexus', keyFileVariable: 'PEM')
				]) {
					sh "ssh -T -i ${PEM} -o StrictHostKeyChecking=no ec2-user@ec2-34-244-126-165.eu-west-1.compute.amazonaws.com rm /home/ec2-user/SK_Tama_Black_JPEG.jpg"
					sh "ssh -T -i ${PEM} -o StrictHostKeyChecking=no ec2-user@ec2-34-244-126-165.eu-west-1.compute.amazonaws.com aws s3 cp s3://fresh-test-bucket/SK_Tama_Black_JPEG.jpg /home/ec2-user/"
					sh "ssh -T -i ${PEM} -o StrictHostKeyChecking=no ec2-user@ec2-34-244-126-165.eu-west-1.compute.amazonaws.com ls /home/ec2-user/"
				}
			}
		}
		stage ('Pull file from bucket in Master') {
			steps {
				withAWS(credentials: 'aws_creds', region: 'eu-west-1') {
					sh 'ls'
					sh 'rm random.txt'
					sh 'ls'
					s3Download bucket: 'fresh-test-bucket', file: 'random.txt', path: 'random.txt'
					sh 'ls'
				}
			}
		}
		stage('Check if file is present on Slave') {
			steps {
				withCredentials([
					sshUserPrivateKey (credentialsId: 'thenexus', keyFileVariable: 'PEM')
				]) {
					sh "ssh -T -i ${PEM} -o StrictHostKeyChecking=no ec2-user@ec2-34-244-126-165.eu-west-1.compute.amazonaws.com pwd"
					sh "ssh -T -i ${PEM} -o StrictHostKeyChecking=no ec2-user@ec2-34-244-126-165.eu-west-1.compute.amazonaws.com ls /home/ec2-user/"
				}
			}
		}
	}
}
