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
                // Se déplacer dans le répertoire du projet
                dir('backend') {
                    // Configurer Node.js (si nécessaire)
                    // tools {
                    //     nodejs 'your-nodejs-tool-name'
                    // }

                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo "Déploiement du projet"
                // Ajoutez les commandes de déploiement ici
            }
        }
    }
}
