pipeline{
    agent any
    stages{
        stage('checkout the code from github'){
            steps{
                 git url: 'https://github.com/Rajeswari-kaakarla/star-agile-insurance-project.git'
                 echo 'github url checkout'
            }
        }
        stage('codecompile with sai'){
            steps{
                echo 'starting compiling'
                sh 'mvn compile'
            }
        }
        stage('codetesting with sai'){
            steps{
                sh 'mvn test'
            }
        }
        stage('qa with sai'){
            steps{
                sh 'mvn checkstyle:checkstyle'
            }
        }
        stage('package with sai'){
            steps{
                sh 'mvn package'
            }
        }
        stage('run dockerfile'){
          steps{
               sh 'docker build -t kaakarla/insuranceproject:1 .'
           }
         }
        stage('Login to dockerhub and push the file'){
            steps{
                withCredentials([string(credentialsId: 'dockerhubpasswd', variable: 'dockerhub')]) {
                  sh 'docker login -u kaakarla -p ${dockerhubpass}'}
            }
        }
        stage('Deployment using Ansible'){
            steps{
                ansiblePlaybook credentialsId: 'ansible', disableHostKeyChecking: true, installation: 'Ansible', inventory: '/etc/ansible/hosts', playbook: 'ansible-playbook.yml', sudo: true, vaultTmpPath: ''
            }
        }
    }
}
