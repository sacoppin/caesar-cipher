pipeline {
    agent any

    stages {
        stage('test') {
            steps {
                sh 'gradle test'
            }
        }
        stage('build') {
            steps {
                echo 'gradle build'
            }
        }
        stage('Release') {
            steps {
                echo 'Releasing....'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}