def summary = "Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})"
pipeline { 
	environment {
      //Values must be specified for the following variables depending on project.   

		GITHUB_URL = 'https://github.com/smflores-07/test2.git'
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
				//colorName: YELLOW , colorCode: #FFFF00
					slackSend (channel: "${SLACK_CHANNEL}", teamDomain: 'test-ldp4148', color: '#FFFF00', message: "STARTED: ${summary}", tokenCredentialId: "${SLACK_TOKEN_ID}", username: '')
					
					scmVars = checkout([$class: 'GitSCM', branches: [[name: "dev"]], userRemoteConfigs: [[url: "${GITHUB_URL}"],[credentialsId: "${JENKINS_CREDENTIALS_ID}"]]])
					
					
				}
			}
			}
		
	post{
			always{
			
				//colorName: GREEN , colorCode: #00FF00
					slackSend (channel: "${SLACK_CHANNEL}", teamDomain: 'test-ldp4148', color: '#00FF00', message: "SUCCESSFUL: ${summary}", tokenCredentialId: "${SLACK_TOKEN_ID}", username: '')
		
            }
	}
}

