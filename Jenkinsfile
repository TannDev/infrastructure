#!/usr/bin/env groovy

pipeline {
    agent {
        label 'kubectl'
    }

    stages {
        stage('Deploy Configuration') {
            when {
                branch 'master'
            }
            steps {
                withKubeConfig([
                        credentialsId: 'microservices-kubernetes-token',
                        serverUrl: "$MICROSERVICES_KUBERNETES_SERVER"
                ]) {
                    // Deploy configurations
                    sh 'kubectl apply -f cert-issuer.yaml'
                    sh 'kubectl apply -f jenkins-account.yaml'
                }
            }
        }
    }
}
