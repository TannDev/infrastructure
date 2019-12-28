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
                    // TODO Deploy configuration changes
                    sh 'kubectl get pods -A'
                }
            }
        }
    }
}