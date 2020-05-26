pipeline {
	agent any

	parameters {
		string (
			defaultValue: "Root",
			description: "just a parameter for database root",
			name: "REQUIRE_TYPE"
			)
	}
	environment {
		JSON_FILE = "Parameters/new-test.json"
		TYPE = "${params.REQUIRE_TYPE}"
	}
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
				script {
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
		}

		// [
		// {
		// 	"something": "other",
		// 	"somethingelse": "otherelse"
		// },{
		//
		// }
		// ]

		stage('Where am I ?') {
			steps {
				sh 'pwd'
			}
		}
		stage('Read file') {
			steps {
				script {
					// put a varaible in here
					def text = readJSON file: JSON_FILE
					// put a variable in here
					out = text['${TYPE}'][0]['Branch'][0][KEY]
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
