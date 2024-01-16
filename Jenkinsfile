pipeline {
    agent any
    parameters {
        choice(name: 'ACTION', choices: ['Deploy', 'Destroy'], description: 'Select the action to perform')
    }
    stages {
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
