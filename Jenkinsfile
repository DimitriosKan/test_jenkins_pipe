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
		JSON_FILE = "${WORKSPACE}/Parameters/new-test.json"
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
[
{
	"something": "other",
	"somethingelse": "otherelse"
},{
	"something": "other",
	"somethingelse": "otherelse"
}
]
					'''
				}
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
					// put a varaible in here
					def text = readJSON file: JSON_FILE
					// put a variable in here
					out = text[TYPE][0]['Branch'][0]['Key']
					echo out
				}
			}
		}
// 				sh (returnStatus: true, script: 'gcloud compute instances list --format="json"')
		stage('Test for readJSON text') {
			steps {
				script {
					RAW = sh (returnStdout: true, script:'gcloud compute instances list --format="json"')
					// echo is working AND getting the correct output
					// echo RAW
					def text = readJSON text: RAW['cpuPlatform']
					echo text
					out = text['cpuPlatform']
					echo out
				}
			}
		}
	}
}
