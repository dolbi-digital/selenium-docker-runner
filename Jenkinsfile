pipeline{
	agent any
	tools {
              dockerTool 'docker3'
              dockerTool 'docker-compose1'
            }
	stages{
		stage("Pull Latest Image"){
			steps{
				sh "docker pull heretic13/selenium-docker"
			}
		}
		stage("Start Grid"){
			steps{
				sh "docker-compose up -d hub chrome firefox"
			}
		}
		stage("Run Test"){
			steps{
				sh "docker-compose up search-module book-flight-module"
			}
		}
	}
	post{
		always{
			archiveArtifacts artifacts: 'output/**'
			sh "docker-compose down"
			sh "sudo rm -rf output/"
		}
	}
}