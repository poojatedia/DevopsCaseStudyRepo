pipeline {
	agent any
	stages{
		stage('Deployment to development server'){
			steps{
				build 'DevelopmentPooja'				
			}			
		}		
		stage('Approval for deploying on test server'){			
			steps{
				mail to: 'neha.verma@kpit.com',subject: "Job '${JOB_NAME}' (${BUILD_NUMBER}) is waiting for input",body: "Please go to ${BUILD_URL}console and verify the build"
				timeout(time:2,unit:'DAYS'){
					input message:'Please approve this request for deployment on test server',submitter:'nehaverma'
				}
			}
		}
		stage('Deployment to testing server'){
			steps{
				build 'TestPooja'
			}
		}
		stage('Approval for deploying on production server'){
			steps{
				mail to: 'vijay.phalak@kpit.com',subject: "Job '${JOB_NAME}' (${BUILD_NUMBER}) is waiting for input",body: "Please go to ${BUILD_URL}console and verify the build"
				timeout(time:2,unit:'DAYS'){
					input message:'Please approve this request for deployment on production server',submitter:'vijayphalak'
				}
			}
		}
		stage('Deployment to production server'){
			steps{
				build 'ProdPooja'
			}
		}
	}
	post{
			success{
				mail to: 'vijay.phalak@kpit.com,poojatedia.kpit.com,neha.verma@kpit.com',subject: "Job '${JOB_NAME}' (${BUILD_NUMBER}) success",body: "Job get sucess"
			}
		}
}