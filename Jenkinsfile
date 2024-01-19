pipeline {
    agent any
    parameters {
        choice(name: 'ACTION', choices: ['Deploy', 'Destroy'], description: 'Select the action to perform')
    }
    stages {
        stage('Authenticate') {
            steps {
                // Set the KUBECONFIG environment variable to the path of the ~/.kube/config file
                sh 'export KUBECONFIG=~/.kube/config'
                
                // Convert the kubeconfig file to use Azure Managed Service Identity (MSI)
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
                        sh 'helm upgrade --install simple-web simple-web --namespace josh --kubeconfig /home/azureuser/.kube/config'
                    } else if (params.ACTION == 'Destroy') {
                        sh 'helm delete simple-web --namespace josh --kubeconfig /home/azureuser/.kube/config'
                    }
                }
            }
        }
    }
}
