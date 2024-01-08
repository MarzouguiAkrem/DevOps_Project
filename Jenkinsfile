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

         stages {
        stage('Checkout') {
            steps {
                // Récupérer le code depuis le référentiel Git
                git branch: 'master', url: 'https://github.com/your-username/DevOps_project.git'
            }
        }
    }
}
