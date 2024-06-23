pipeline{
    agent{
        label 'AGENT-1'
    }
    options{
        timeout(time: 30, unit: 'MINUTES')
        ansiColor('xterm')
    }
    parameters {
        choice(name: 'command', choices: ['Apply', 'Destroy'], description: 'Pick something')
    }
    stages{
        stage('init'){
            steps{
                sh 'cd daws-jenkins/044/solution/terraform/'
                sh 'terraform init -reconfigure'
            }
            when {
                expression { params.command == "Apply"}
            }
        }
        stage('plan'){
            steps{
                sh 'cd daws-jenkins/044/solution/terraform/'
                sh 'terraform plan'
            }
            when {
                expression { params.command == "Apply"}
            }
        }
        stage('apply'){
            input {
                message "Should we continue with apply command?"
                ok "Yes, we should."
            }
            when {
                expression { params.command == "Apply"}
            }
            steps{
                sh 'cd daws-jenkins/044/solution/terraform/'
                sh 'terraform apply -auto-approve'
            }
        }
        stage('destroy'){
            input {
                message "Should we continue with destroy command?"
                ok "Yes, we should."
            }
            when {
                expression { params.command == "Destroy"}
            }
            steps{
                sh 'cd daws-jenkins/044/solution/terraform/'
                sh 'terraform destroy -auto-approve'
            }
        }
    }
    post{
        success{
            echo 'SUCCESS'
        }
        failure{    
            echo 'FAILED'
        }
    }
}