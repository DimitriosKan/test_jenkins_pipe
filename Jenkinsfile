pipeline {
	agent any

	def awsSecretMasterID = [
		"mapKey": "mapValue"
	]

	parameters {
		string (
			defaultValue: "Root",
			description: "just a parameter for database root",
			name: "REQUIRE_TYPE"
			)

		choice(
			choices: [
			"mapKey"
			],
			name: "RDSArnNameSQLSERVER"
		)

	}
	environment {
		awsRDSArnNameSQLSERVER = "${params.RDSArnNameSQLSERVER}"
		JSON_FILE = "${WORKSPACE}/Parameters/new-test.json"
		TYPE = "${params.REQUIRE_TYPE}"
		TEST_FILE = "${WORKSPACE}/test.json"
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
					sh 'cat test.json'
				}
			}
		}

		stage('Where am I ?') {
			steps {
				sh 'pwd'
			}
		}
		stage('Cut up a string') {
			steps {
				script {
					def stringname = "daf-prod-something-rds-prod-secrets"
					def splitstring = stringname.split("-")
					echo "Swag test below: ${splitstring[2]}"
				}
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
		stage('Edit file') {
			steps {
				script {
					sh '''
						sed -i -e "s/other//g" "${TEST_FILE}"
					'''
				}
			}
		}
		stage('Mapping Test') {
			steps {
				script {
					def awsSecretMasterIDValue = "${awsSecretMasterID.awsRDSArnNameSQLSERVER}"

					echo awsSecretMasterIDValue
				}
			}
		}



// 				sh (returnStatus: true, script: 'gcloud compute instances list --format="json"')
		// stage('Test for readJSON text') {
		// 	steps {
		// 		script {
		// 			RAW = sh (returnStdout: true, script:'gcloud compute instances list --format="json"')
		// 			// echo is working AND getting the correct output
		// 			echo RAW
		// 			def text = readJSON text: RAW[0]['cpuPlatform']
		// 			echo text
		// 			out = text['cpuPlatform']
		// 			echo out
		// 		}
		// 	}
		// }
	}
}
