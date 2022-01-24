pipeline {
    agent any

    stages {
        stage('test') {
            steps {
                sh './gradlew test'
            }
        }
        stage('build') {
            steps {
                echo './gradlew build'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}