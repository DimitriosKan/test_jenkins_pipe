pipeline {
	agent any
	options {
		ansiColor("xterm")
		buildDiscarder(logRotator(numToKeepStr:"5"))
		disableConcurrentBuilds()
		timeout(time: 15, unit: "MINUTES")
		timestamps()
	}
	stages {
		stage('Just a Test Stage') {
			steps {
				script {
					ansiColor("xterm")
					echo 'Test stage ...'
				}
			}
		}
		stage('Just a Test Stage V2') {
			steps {
				script {
					ansiColor("xterm")
					echo 'Test stage ...'
				}
			}
		}
	}
}
