pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                echo 'Récupération du code'
            }
        }

        stage('Build Docker') {
            steps {
                bat 'docker build -t dev .'
            }
        }
        
        stage('Deploy Kubernetes') {
            steps {
        bat 'kubectl apply -f k8s/deployment.yaml'
        bat 'kubectl apply -f k8s/service.yaml'
            }
        }

        stage('Run Docker') {
            steps {
                bat 'docker rm -f monsite || exit 0'
                bat 'docker run -d -p 8090:80 --name monsite dev'
            }
        }
    }
}
