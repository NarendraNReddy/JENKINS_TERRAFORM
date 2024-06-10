pipeline {
    agent {
        label 'AGENT-1'
    }

    options {
        // Timeout counter starts AFTER agent is allocated
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
        ansiColor('xterm')
    }

    stages {
        stage('Init') { 
            steps {
                sh """
                 cd 01-vpc
                 terraform init -reconfigure
                """
                
            }
        }
        stage('Plan') { 
            steps {
                sh """
                 cd 01-vpc
                 terraform plan
                """              
            }
        }
        stage('Deploy') { 
            input {
                message "Should we continue?"
                ok "Yes, we should."
            }     
                   
            steps {
                sh """
                 cd 01-vpc
                 terraform apply -auto-approve
                """
            }
        }
        stage('Print params'){
            steps {
                echo "Hello ${params.PERSON}"
                echo "Biography: ${params.BIOGRAPHY}"
                echo "Toggle: ${params.TOGGLE}"
                echo "Choice: ${params.CHOICE}"
                echo "Password: ${params.PASSWORD}"
                echo "triggered test2"
                
            }            
        }

    }
    post { 
        always { 
            echo 'I will always say Hello again!'
            deleteDir()
        }
        success { 
            echo 'I will run when pipeline is success'
        }
        failure { 
            echo 'I will run when pipeline is failure'
        }
    }    
}