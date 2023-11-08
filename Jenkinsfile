pipeline{
    agent any
    stages{
        stage("getting code") {
            steps {
                git url: 'https://github.com/Louaykharouf26/VM_Monitoring.git', branch: 'master',
                credentialsId: 'github-credentials' //jenkins-github-creds
                sh "ls -ltr"
            }
        }
       stage("Create the VM") {
            steps {                
                script {
                    echo "======== executing ========"
                        sh "pwd"
                        sh "terraform init"
                        sh "terraform apply --auto-approve --var-file=./terraform.tfvars.json"
                         }            
                        }
                    } 
                stage("Ansible Playbooks") {
            steps {                
                script {
                    echo "======== executing ========"
                        sh "pwd"
                        sh "ansible-playbook -i hosts update-hosts.yml"
                        sh "ansible-playbook -i hosts install_prometheus.yml"
                        sh "ansible-playbook -i hosts install_grafana.yml"
                         }            
                        }
                    } 
                }
            post{
                success{
                    echo "======== Setting up infra executed successfully ========"
                }
                failure{
                    echo "======== Setting up infra execution failed ========"
                }
            }
             
        }          
   /* 
    post{
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }*/
