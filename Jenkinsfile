pipeline {
    agent any
    
    stages {
        stage('Clone Repository') {
            steps {
                echo '📥 Clonage du dépôt GitHub...'
                git branch: 'main',
                    url: 'https://github.com/VOTRE_USERNAME/student-management.git'
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
        }
        
        stage('Package') {
            steps {
                echo '📦 Création du package...'
                sh 'mvn package'
            }
        }
    }
    
    post {
        success {
            echo '✅ Pipeline exécuté avec succès !'
        }
        failure {
            echo '❌ Le pipeline a échoué.'
        }
    }
}
