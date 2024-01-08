pipeline {
    agent any

    triggers {
        pollSCM('*/5 * * * *') // Vérifier toutes les 5 minutes
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Récupération du code source"
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Build du projet"
                // Ajoutez les commandes de build ici

                // Exemple pour un projet Node.js (à adapter selon votre projet)
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                echo "Déploiement du projet"
                // Ajoutez les commandes de déploiement ici

                // Exemple pour le déploiement sur Kubernetes
                sh 'kubectl apply -f k8s/deployment.yaml -n your-namespace'
                sh 'kubectl rollout status deployment/your-deployment-name -n your-namespace'
            }
        }
    }
}
