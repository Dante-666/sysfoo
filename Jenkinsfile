pipeline {
	agent any

	tools {
		maven '3.8.1'
	}

	stages {

		stage('build') {
			steps {
				sh 'mvn compile'
			}
		}

		stage('test') {
			steps {
				sh 'mvn clean test'
			}
		}

		stage('package') {
			steps {
				sh 'mvn package -DskipTests'
			}
		}
	}
}
