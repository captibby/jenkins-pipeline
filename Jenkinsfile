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

        stage('Deploy') {
            steps {
                script {
                    // Copy the HTML file to the workspace, where the server will serve it from
                    sh 'cp index.html .'
                    // Start the Python HTTP server in the background
                    sh 'python3 server.py &'
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
