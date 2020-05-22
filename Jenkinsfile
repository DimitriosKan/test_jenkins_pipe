pipeline {
	agent any

	stages {
		stage('Just a Test Stage') {
			steps {
				script {
					echo 'Test stage ...'
				}
			}
		}
		stage('Trollolol') {
			steps {
				sh 'pwd'
			}
		}
		stage('Test for readJSON') {
			steps {
				script {
					text = readJSON text: 'gcloud compute instances list --format="json"'
					echo '${text}'
				}
			}
		}
	}
}
