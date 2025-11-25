pipeline {
    agent any
    
    triggers {
        pollSCM('H/2 * * * *')  // Vérifie GitHub toutes les 2 minutes
    }
    
    environment {
        DOCKERHUB_USER = 'asma0000/devops'
        IMAGE_NAME = 'student-management'
    }
    
    stages {
        
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Asma0002/AsmaCherni4SIM1'
            }
        }
        
        stage('Maven Compile') {
            steps {
                sh 'mvn compile'
            }
        }
        
        stage('Maven Package') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh """
                    docker build -t ${DOCKERHUB_USER}/${IMAGE_NAME}:latest .
                    docker tag ${DOCKERHUB_USER}/${IMAGE_NAME}:latest ${DOCKERHUB_USER}/${IMAGE_NAME}:${BUILD_NUMBER}
                """
            }
        }
        
        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials',
                                                 usernameVariable: 'USER',
                                                 passwordVariable: 'PASS')]) {
                    sh """
                        echo "\$PASS" | docker login -u "\$USER" --password-stdin
                    """
                }
            }
        }
        
        stage('Docker Push') {
            steps {
                sh """
                    docker push ${DOCKERHUB_USER}/${IMAGE_NAME}:latest
                    docker push ${DOCKERHUB_USER}/${IMAGE_NAME}:${BUILD_NUMBER}
                """
            }
        }
    }
    
    post {
        success {
            echo '✅ Build réussi ! Image Docker créée et poussée sur Docker Hub.'
        }
        failure {
            echo '❌ Le build a échoué. Vérifiez les logs.'
        }
        always {
            sh 'docker logout'
        }
    }
}
