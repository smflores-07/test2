pipeline { 
	environment {
      //Values must be specified for the following variables depending on project.   

		//PROJECT_NAME = 'sample-project'
		//MAIN_POM_LOCATION = 'application1'
		//BITBUCKET_URL = 'https://github.com/smflores-07/test2.git/'
		//multiple Jira tickets should be comma-separated 
		
		SLACK_CHANNEL='test'
		SLACK_TOKEN_ID='test-ldp4148'
		
	}
	agent any
		options {
			skipDefaultCheckout( true )
		}
		stages{
			stage('Checkout Project') {
				steps{
				/*
					googlechatnotification(
						url: env.GOOGLE_CHAT_URL,
						message: "\\n*BUILD STARTED* - " + new Date(currentBuild.startTimeInMillis).format("MMM dd, yyyy h:mm a", TimeZone.getTimeZone("GMT+8:00")),
						sameThreadNotification: 'true'
					)
				*/
					//colorName: YELLOW , colorCode: #FFFF00
					slackSend (channel: "${SLACK_CHANNEL}", color: '#FFFF00', message: "STARTED: " + new Date(currentBuild.startTimeInMillis).format("MMM dd, yyyy h:mm a", TimeZone.getTimeZone("GMT+8:00")), tokenCredentialId: "${SLACK_TOKEN_ID}", username: '')
					/*
					script {
						//DIRECTORY CREATION
						//set project directory
						projDir = env.PARENT_FOLDER + "/" + env.PROJECT_NAME
						projJobDir = projDir + "/" + env.MAIN_POM_LOCATION
						
						//re-create project/job folder
						fileOperations([folderDeleteOperation(folderPath: projDir)])
						fileOperations([folderCreateOperation(folderPath: projDir)])
					
						scmVars = checkout([$class: 'GitSCM', branches: [[name: env.BRANCH_NAME]], extensions: [[$class: 'PathRestriction', excludedRegions: '', includedRegions: "${MAIN_POM_LOCATION}/.*"]], userRemoteConfigs: [[credentialsId: env.JENKINS_CREDENTIALS_ID, url: env.BITBUCKET_URL]]])
						
						BRANCH="${scmVars.GIT_BRANCH}"
						println "Branch name : ${BRANCH}"
						
						
					}
					*/
				}
			}
			}
		
	post{
			always{
			
				success { 
				//colorName: GREEN , colorCode: #00FF00
					slackSend (channel: "${SLACK_CHANNEL}", color: '#00FF00', message: "SUCCESSFUL", tokenCredentialId: "${SLACK_TOKEN_ID}", username: '')
			}
			failure { 
				//colorName: RED , colorCode: #FF0000
					slackSend (channel: "${SLACK_CHANNEL}", color: '#FF0000', message: "FAILURE", tokenCredentialId: "${SLACK_TOKEN_ID}", username: '')
			}
			aborted { 
				//colorName: GRAY , colorCode: #808080
					slackSend (channel: "${SLACK_CHANNEL}", color: '#808080', message: "ABORTED", tokenCredentialId: "${SLACK_TOKEN_ID}", username: '')
			}
            }
	}
}

