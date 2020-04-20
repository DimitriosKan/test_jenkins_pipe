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
		stage('Initial Test SSH') {
			steps {
				withCredentials([
					sshUserPrivateKey (credentialsId: 'thenexus', keyFileVariable: 'PEM')
				]) {
					sh 'pwd'
					sh "ssh -T -i ${PEM} -o StrictHostKeyChecking=no ec2-user@ec2-34-244-126-165.eu-west-1.compute.amazonaws.com pwd"
					//sh "scp -i ${PEM} -o StrictHostKeyChecking=no /home/ec2-user/push.sh ec2-user@ec2-34-244-126-165.eu-west-1.compute.amazonaws.com:/home/ec2-user/"
					sh "ssh -T -i ${PEM} -o StrictHostKeyChecking=no ec2-user@ec2-34-244-126-165.eu-west-1.compute.amazonaws.com aws s3 cp s3://fresh-test-bucket/SK_Tama_Black_JPEG.jpg /home/ec2-user/"
					sh "ssh -T -i ${PEM} -o StrictHostKeyChecking=no ec2-user@ec2-34-244-126-165.eu-west-1.compute.amazonaws.com ls /home/ec2-user/"
				}
			}
		}
		stage ('Pull file from bucket') {
			steps {
				withAWS(credentials: 'aws_creds', region: 'eu-west-1') {
					s3Download bucket: 'fresh-test-bucket', file: 'random.txt', path: '/home/ec2-user/random.txt'
					sh 'ls'
				}
			}
		}
		stage('Check if file is present') {
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
