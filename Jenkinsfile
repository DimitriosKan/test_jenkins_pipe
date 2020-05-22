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
				sh '''
				cat <<'EOF' > test.json
				{
					"Root": [ {
						"Branch": [
						{"Key": "Value"}
						]
						}]
				}
				'''
			}
		}
		stage('Where am I ?') {
			steps {
				sh 'pwd'
			}
		}
		stage('Read file') {
			steps {
				script {
					def text = readJSON file: 'test.json'
					out = text['Root']
					echo out
				}
			}
		}
// 				sh (returnStatus: true, script: 'gcloud compute instances list --format="json"')
		// stage('Test for readJSON') {
		// 	steps {
		// 		script {
		// 			def text = readJSON text: 'gcloud compute instances list --format="json"'
		// 			echo '${text}'
		// 		}
		// 	}
		// }
	}
}
