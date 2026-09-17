pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                bat 'docker run --rm -v "%CD%:/workspace" -w /workspace gradle:8.14.3-jdk21 gradle build'
            }
        }

        stage('Test') {
            steps {
                bat 'docker run --rm -v "%CD%:/workspace" -w /workspace gradle:8.14.3-jdk21 gradle check'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'build/libs/**/*.jar', fingerprint: true
            junit 'build/reports/**/*.xml'
        }
    }
}
