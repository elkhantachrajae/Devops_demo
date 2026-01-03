pipeline {
    agent any

    tools {
        maven 'Maven-3.9' // Vous devrez configurer Maven dans Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                echo '📥 Récupération du code depuis GitHub...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo '🔨 Compilation du projet...'
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Exécution des tests...'
                sh 'mvn test'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Package') {
            steps {
                echo '📦 Création du JAR...'
                sh 'mvn package -DskipTests'
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline exécuté avec succès!'
        }
        failure {
            echo '❌ Le pipeline a échoué.'
        }
    }
}