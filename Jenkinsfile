pipeline {
	agent any
	environment {
        NEW_VERSION = '1.3.0'
        GITHUB_CREDENTIALS = credentials('github_credentials')
	}
	stages {
		
		stage("checkout") {
			steps{
				echo "checking out the code ${GITHUB_CREDENTIALS}"
			}
			
		}
		
		stage("build") {
			steps{
				echo "building out the code"
				echo "building version ${NEW_VERSION}"
			}
		}
		
		stage("test") {
            when {
                expression {
                    BRANCH_NAME != 'main'
                }
            }
			steps{
				echo "testing out the code"
			}
		}
		
		stage ("deploy") {

			steps{
                echo "deploying out the code"
                withCredentials([
                    usernamePassword(
                        credentials : "SERVER_CREDENTIALS",
                        usernameVariable: USER,
                        passwordVariable: PWD)
                ]) {
                    echo "${USER}"
                	echo "${PWD}"
                }


			}
		}

	}
		post {
			always {
                echo "Executing the POST BUILD STEP."
			} 
			failure {
			    echo "Executing the POST BUILD STEP on Failure."
			}
		}
}
