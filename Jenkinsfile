pipeline {
    agent any

    stages {
        stage('Deploy t0 k8s') {        //withKubeCredentials: Configure Kubernetes CLI (kubectl) with multiple credentials
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'kubernetes', contextName: '', credentialsId: 'k8s-token', namespace: 'webapps', serverUrl: 'https://172.17.0.232:6443']]) {
                    sh "kubectl apply -f deployment-service.yml"
                    sleep 60
                }
            }
        }
        stage('Verify Deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'kubernetes', contextName: '', credentialsId: 'k8s-token', namespace: 'webapps', serverUrl: 'https://172.17.0.232:6443']]) {
                    sh "kubectl get all -n webapps"
                }
            }
        }
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
    }
}
