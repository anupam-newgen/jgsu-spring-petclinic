pipeline {
	agent any
	parameters {
	    string(name: 'VERSION', defaultValue: '', description: 'Version to be deployed on prod.')
	    choice(name: 'VERSION1', choices: ['1', '2', '3'], description: 'Version to be deployed on prod.')
	    booleanParam(name: 'executeTests', defaultValue: false, description: 'Executes tests or not.')
	}
	tools {
	    Maven 'maven'
	}
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
                    ${executeTests}
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
