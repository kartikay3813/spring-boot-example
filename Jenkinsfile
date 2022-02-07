pipeline { 
    agent any  
    
    tools { 
        maven 'Maven'  
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
                failure
                {
                    mail( body: 'Deliver Stage FAILED', subject: 'Build Report Test stage', to: 'kartikay.bhardwaj@knoldus.com' )
                }
                success
                {
                    mail( body: 'Deliver Stage succeeded', subject: 'Build Report Test stage', to: 'kartikay.bhardwaj@knoldus.com' )
                }
                
            }
        }
        stage('Deliver') {
            when {
                expression {
                    BRANCH_NAME == 'Production'
                }
            }
            steps {
                sh 'chmod +x ./jenkins/scripts/deliver.sh'
                sh './jenkins/scripts/deliver.sh'
            }
            post {
                failure
                {
                    mail( body: 'Deliver Stage FAILED', subject: 'Build Report Deliver stage', to: 'kartikay.bhardwaj@knoldus.com' )
                }
                 success
                {
                    mail( body: 'Deliver Stage succeeded', subject: 'Build Report Deliver stage', to: 'kartikay.bhardwaj@knoldus.com' )
                }
            }
        }
    }
}
