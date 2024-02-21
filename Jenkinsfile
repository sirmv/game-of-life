pipeline {
	agent any
	triggers {
		cron('0 * * * *')
	}
	stages {
		stage ('SourceCode') {
			steps {
				git url: 'https://github.com/niranjanakoni/game-of-life.git', branch: 'master'
			}
		}
		stage ('Build the code') {
			steps {
				sh script: 'mvn clean package'
			}
		}
		stage ('Copying Artifact to Tomcat') {
                        steps {
                                sh script: 'sudo cp /home/user1/jenkins_root/workspace/game-of-life/gameoflife-web/target/*.war /opt/tomcat/webapps'
                        }
                }
		stage ('Reporting & Archiving') {
			steps {
				 junit testResults: 'gameoflife-web/target/surefire-reports/*.xml'
			}
		}
	}
	post {
		success {
			echo "Success"
		}
		unsuccessful {
			echo "Failure"
		}
	}
}
