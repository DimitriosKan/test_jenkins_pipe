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
		stage('Populate file') {
			steps {
				sh (returnStatus: true, script: 'gcloud compute instances list --format="json" > ./test.txt')
				sh 'cat ./test.txt'
			}
		}
		stage('Read file') {
			steps {

			}
		}
		stage('Test for readJSON') {
			steps {
				script {
					def text = readJSON text: 'gcloud compute instances list --format="json"'
					echo '${text}'
				}
			}
		}
	}
}
