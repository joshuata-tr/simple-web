pipeline {
    agent any
    parameters {
        choice(name: 'ACTION', choices: ['Deploy', 'Destroy'], description: 'Select the action to perform')
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/joshuata-tr/simple-web.git'
            }
        }
        stage('Build') {
            steps {
                dir('/home/azureuser/simple-web-chart') {
                    sh 'helm package simple-web/simple-web'
                    sh 'helm repo index . --url https://joshuata-tr.github.io/simple-web'
                }
            }
        }
        stage('Deploy or Destroy') {
            steps {
                script {
                    if (params.ACTION == 'Deploy') {
                        sh 'helm repo add simple-web https://joshuata-tr.github.io/simple-web'
                        sh 'helm upgrade --install simple-web simple-web/simple-web'
                    } else if (params.ACTION == 'Destroy') {
                        sh 'helm delete simple-web'
                    }
                }
            }
        }
    }
}
