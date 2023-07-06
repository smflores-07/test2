pipeline { 
	environment {
      //Values must be specified for the following variables depending on project.   

		//PROJECT_NAME = 'sample-project'
		//MAIN_POM_LOCATION = 'application1'
		GITHUB_URL = 'https://github.com/smflores-07/test2.git/'
		JENKINS_CREDENTIALS_ID = 'smflores-07'
		
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
					slackSend (channel: "${SLACK_CHANNEL}", teamDomain: 'test-ldp4148', color: '#FFFF00', message: "STARTED: " + new Date(currentBuild.startTimeInMillis).format("MMM dd, yyyy h:mm a", TimeZone.getTimeZone("GMT+8:00")), tokenCredentialId: "${SLACK_TOKEN_ID}", username: '')
					
					script {
						//re-create project/job folder
						
						scmVars = checkout([$class: 'GitSCM', branches: [[name: env.BRANCH_NAME]], userRemoteConfigs: [[credentialsId: env.JENKINS_CREDENTIALS_ID, url: env.GITHUB_URL]]])
						
						BRANCH="${scmVars.GIT_BRANCH}"
						println "Branch name : ${BRANCH}"
						
						
					}
					
				}
			}
			}
		
	post{
			always{
			
				//colorName: GREEN , colorCode: #00FF00
					slackSend (channel: "${SLACK_CHANNEL}", teamDomain: 'test-ldp4148', color: '#00FF00', message: "SUCCESSFUL", tokenCredentialId: "${SLACK_TOKEN_ID}", username: '')
		
            }
	}
}

