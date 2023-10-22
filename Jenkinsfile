pipeline {
    agent any

    stages {
        stage('Prepare Environment') {
            steps {
                script {
                    // Clean workspace
                    cleanWs()
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    // Nothing to build for a static HTML page
                    echo 'Build stage completed.'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Start a simple Python HTTP server to serve the static HTML page
                    sh 'python3 -m http.server 8000 &'
                }
            }
        }
    }

    post {
        always {
            // Optionally, add steps to clean up after the pipeline runs
            echo 'Pipeline completed.'
        }
    }
}
