def summary = "Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})"
pipeline { 
	environment {
      //Values must be specified for the following variables depending on project.   

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
				//colorName: YELLOW , colorCode: #FFFF00
					slackSend (channel: "${SLACK_CHANNEL}", teamDomain: 'test-ldp4148', color: '#FFFF00', message: "STARTED: ${summary}", tokenCredentialId: "${SLACK_TOKEN_ID}", username: '')
					
					checkout([$class: 'GitSCM', branches: [[name: '*/dev']], extensions: [], userRemoteConfigs: [[credentialsId: 'smflores-07', url: 'https://github.com/smflores-07/test2.git']]])
					
					
				}
			}
			}
		
	post{
	
		success { 
			//colorName: GREEN , colorCode: #00FF00
				slackSend (channel: "${SLACK_CHANNEL}", teamDomain: 'test-ldp4148', color: '#00FF00', message: "SUCCESSFUL: ${summary}", tokenCredentialId: "${SLACK_TOKEN_ID}", username: '')
		}
		failure { 
			//colorName: RED , colorCode: #FF0000
				slackSend (channel: "${SLACK_CHANNEL}", teamDomain: 'test-ldp4148', color: '#FF0000', message: "FAILURE: ${summary}", tokenCredentialId: "${SLACK_TOKEN_ID}", username: '')
		}
		aborted { 
			//colorName: GRAY , colorCode: #808080
				slackSend (channel: "${SLACK_CHANNEL}", teamDomain: 'test-ldp4148', color: '#808080', message: "ABORTED: ${summary}", tokenCredentialId: "${SLACK_TOKEN_ID}", username: '')
		}
	}
}

