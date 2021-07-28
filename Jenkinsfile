pipeline {
  agent none
  stages {
    stage('build') {
      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      steps {
        sh 'mvn compile'
      }
    }

    stage('test') {
      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      steps {
        sh 'mvn clean test'
      }
    }

		if (env.BRANCH_NAME == 'master') {
			stage('package') {
				agent {
					docker {
						image 'maven:3.6.3-jdk-11-slim'
					}

				}
				steps {
					sh 'mvn package -DskipTests'
					archiveArtifacts 'target/*.war'
				}
			}

			stage('Docker BnP') {
				agent any
				steps {
					script {
						docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {
							def dockerImage = docker.build("siddharthjsingh/sysfoo:v${env.BUILD_ID}", "./")
							dockerImage.push()
							dockerImage.push("latest")
							dockerImage.push("dev")
						}
					}

				}
			}

		}

  }
  tools {
    maven '3.8.1'
  }
}
