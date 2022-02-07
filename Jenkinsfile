pipeline{
    agent any 
        
    tools { 
        maven '/usr/share' 
    }
    stages{
	    
        stage("building"){
            steps{
                sh "mvn compile"
		 
            }
        }
	 stage('Testing') {
            steps {
                echo 'Testing the application'
                sh "mvn test"
            }
        }


    }
    post{
        always{
            mail to: 'kartikay.bhardwaj@knoldus.com',
			subject: "Pipeline: ${currentBuild.fullDisplayName} is ${currentBuild.currentResult}",
			body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}"
        }
        success{
            echo "Pipeline executed successfully.."
        }
        failure{
            echo "Pipeline execution failed.."
        }
    }
}
