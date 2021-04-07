pipeline{
	agent any
	tools{
		jdk 'my_java'
		maven 'my_maven'
	}
	stages{
		stage('clone_repo'){
			steps{
				echo 'cloning the git repo'
				git credentialsId: 'cf5aa903-75a6-4df6-85fa-4d254d9c9e4b', url: 'https://github.com/mmudireddy/DevOpsClassCodes'
			}
		}
		stage('compile'){
			steps{
				echo 'compiling source code'
				sh 'mvn compile'
			}
		}
		stage('code_review){
		      steps{
			      echo 'performing code review'
			      sh 'mvn pmd:pmd'
		      }
		}      
		stage('code_testing'){
			steps{
				echo 'testing the code'
				sh 'mvn test'
			}
			post{
				success{
					junit 'target/surefire-reports/*.xml'
				}
			}
		}
		stage('code_coverage'){
			steps{
				echo 'checking the code coverage'
				sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
			}
			post{
				success{
					cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
				}
			}
		}
		stage('package'){
			steps{
				echo 'packaging the code'
				sh 'mvn package'
			}
			post{
				always{
					echo 'Hurray! finished packaging the code'
				}
			}
		}
	}
 }
		      
			      
			      
