pipeline {
    agent any

    environment {
        CHART_NAME = "simple-web"
        CHART_REPO = "https://github.com/joshuata-tr/simple-web"
        NAMESPACE = "josh"
    }

    stages {
        stage('Deploy Chart') {
            steps {
                sh "helm repo add acr https://acrinterview.azurecr.io/helm/v1/repo"
                sh "helm repo update"
                sh "helm upgrade --install ${CHART_NAME} ${CHART_REPO} --namespace ${NAMESPACE}"
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
