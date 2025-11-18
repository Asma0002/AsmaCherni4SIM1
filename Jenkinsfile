pipeline {
    agent any
    stages {
        stage('hello') {
            steps {
                echo 'Bienvenue dans le pipeline Jenkins !'
                git branch: 'main', url: 'https://github.com/Asma0002/AsmaCherni4SIM1'
            }
        }
        stage('compilation') {
            steps {
                echo 'Compilation du projet...'
                sh 'mvn clean install -DskipTests'
            }
        }
    }
}
