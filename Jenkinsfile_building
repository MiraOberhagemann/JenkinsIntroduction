pipeline{
	agent any
	stages{
		stage('Preparing'){
			steps {
				echo "I'm in stage Preparing!"
				deleteDir()
				checkout scm
				script {
					// Get commit parameters like commit code and author
					env.SHORT_COMMIT_CODE = sh(returnStdout: true, script: "git log -n 1 --pretty=format:'%h'").trim()
					env.COMMIT_MESSAGE = sh(returnStdout: true, script: "git log --format=%B -n 1 ${SHORT_COMMIT_CODE}").trim()
					env.COMITTER_EMAIL = sh(returnStdout: true, script: 'git --no-pager show -s --format=\'%ae\'').trim()
					env.AUTHOR_NAME = sh(returnStdout: true, script: 'git --no-pager show -s --format=\'%an\'').trim()
					// Set build name and description accordingly
					currentBuild.displayName = "Commit ${SHORT_COMMIT_CODE} | ${AUTHOR_NAME}"
					currentBuild.description = "${COMMIT_MESSAGE}"
					echo "Finished getting files from github repository"
				}
			}
		}
		stage('Build'){
			steps {
				echo "I'm in stage Build!"
				sh '''
					chmod +x *.sh
					./start.sh
					cmake ./sourcefiles
					make
				'''
				echo "Finished building"
			}
		}
		stage('Testing'){
			steps {
				echo "I'm in stage Testing!"
				
				echo "Finished testing"
			}
		}
		stage('Deploying'){
			steps {
				echo "I'm in stage Deploying!"
				
				echo "Finished Deploying!"
			}
		}
	}
}