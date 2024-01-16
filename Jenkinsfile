pipeline {
    agent any
    parameters {
        choice(name: 'ACTION', choices: ['Deploy', 'Destroy'], description: 'Select the action to perform')
    }
    stages {
        stage('Authenticate') {
            steps {
                sh 'az aks get-credentials -n devops-interview-aks -g devops-interview-rg'
                sh 'export KUBECONFIG=~/.kube/config'
                sh 'kubelogin convert-kubeconfig -l msi'
            }
        }
        stage('Checkout') {
            steps {
                git 'https://github.com/joshuata-tr/simple-web.git'
            }
        }
        stage('Deploy or Destroy') {
            steps {
                script {
                    if (params.ACTION == 'Deploy') {
                        sh 'helm upgrade --install simple-web simple-web'
                    } else if (params.ACTION == 'Destroy') {
                        sh 'helm delete simple-web'
                    }
                }
            }
        }
    }
}
