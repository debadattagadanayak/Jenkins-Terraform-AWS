pipeline {

    parameters {
        booleanParam(name: 'autoApprove', defaultValue: false, description: 'Automatically run apply after generating plan?')
    } 
    environment {
        AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
    }

   agent  any
    stages {
        stage('checkout') {
            steps {
                 script{
                        dir("terraform")
                        {
                            git "https://github.com/debadattagadanayak/Jenkins-Terraform-AWS.git"
                        }
                    }
                }
            }

        stage('Plan') {
            steps {
                sh 'sudo yum install -y wget unzip'
                sh 'sudo wget https://releases.hashicorp.com/terraform/1.0.8/terraform_1.0.8_linux_amd64.zip ; sudo unzip terraform_1.0.8_linux_amd64.zip -d /usr/local/bin/'
                sh 'sudo rm terraform_1.0.8_linux_amd64.zip'
                sh 'echo 'export PATH=$PATH:/usr/local/bin' >> ~/.bashrc'
                sh 'pwd;cd terraform/ ; terraform init'
                sh "pwd;cd terraform/ ; terraform plan -out tfplan"
                sh 'pwd;cd terraform/ ; terraform show -no-color tfplan > tfplan.txt'
            }
        }
        stage('Approval') {
           when {
               not {
                   equals expected: true, actual: params.autoApprove
               }
           }

           steps {
               script {
                    def plan = readFile 'terraform/tfplan.txt'
                    input message: "Do you want to apply the plan?",
                    parameters: [text(name: 'Plan', description: 'Please review the plan', defaultValue: plan)]
               }
           }
       }

        stage('Apply') {
            steps {
                sh "pwd;cd terraform/ ; terraform apply -input=false tfplan"
            }
        }
    }

  }
