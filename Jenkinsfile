pipeline { 
	environment {
      //Values must be specified for the following variables depending on project.   

		PROJECT_NAME = 'sample-project'
		MAIN_POM_LOCATION = 'application1'
		BITBUCKET_URL = 'https://edo-bitbucket.globe.com.ph:8443/scm/devops/sample-java-project.git'
		//multiple Jira tickets should be comma-separated 
		
		GOOGLE_CHAT_URL = credentials("test-google-chat")
		
	}
	agent any
		options {
			skipDefaultCheckout( true )
		}
		stages{
			stage('Checkout Project') {
				steps{
					googlechatnotification(
						url: env.GOOGLE_CHAT_URL,
						message: "\\n*BUILD STARTED* - " + new Date(currentBuild.startTimeInMillis).format("MMM dd, yyyy h:mm a", TimeZone.getTimeZone("GMT+8:00")) + "\\nPipeline: ${summary}",
						sameThreadNotification: 'true'
					)
					
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
				}
			}
			}
		
	post{
			always{
				googlechatnotification(
					url: env.GOOGLE_CHAT_URL,
					message: "*BUILD " + currentBuild.currentResult + "* - " + new Date(currentBuild.startTimeInMillis + currentBuild.duration).format("MMM dd, yyyy h:mm a", TimeZone.getTimeZone("GMT+8:00")) +"\\n(Duration: " + new Date(currentBuild.duration).format("H:mm:ss", TimeZone.getTimeZone("GMT")) + ")\\nPipeline: ${summary}",
					notifySuccess: 'true',
					notifyFailure: 'true',
					notifyAborted: 'true',
					sameThreadNotification: 'true',
					suppressInfoLoggers: 'true'
				)
            }
	}
}

