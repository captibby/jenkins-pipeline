pipeline {
    agent any

    stages {
        stage('Initialize') {
            steps {
                echo 'Preparing the Environment...'
            }
        }

        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                // Uncomment and adjust the following line if you have a repository to checkout:
                // checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                // Include your build steps here, if applicable.
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Include your test steps here, if applicable.
            }
        }

        stage('Archive Artifacts') {
            steps {
                echo 'Archiving artifacts...'
                // Uncomment and adjust the following line if you have artifacts to archive:
                // archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo 'Deploying...'
                    sh '''
                    # Define the app name and port
                    APP_NAME="my-web-page"
                    PORT="8002"

                    # Identify the container ID for an existing container with the specific image and port
                    CONTAINER_ID=$(docker ps -q --filter "ancestor=${APP_NAME}" --filter "status=running" | xargs docker inspect --format '{{range $p, $conf := .NetworkSettings.Ports}}{{$p}} {{range $conf}}{{.HostPort}}{{end}} {{end}}' | grep "80/tcp" | grep "${PORT}" | awk '{print $1}')

                    if [ ! -z "$CONTAINER_ID" ]; then
                      echo "Stopping and removing the container running on port ${PORT}..."
                      docker stop $CONTAINER_ID
                      docker rm $CONTAINER_ID
                    fi

                    echo 'FROM nginx:alpine' > Dockerfile
                    echo 'COPY index.html /usr/share/nginx/html/index.html' >> Dockerfile

                    docker build -t ${APP_NAME} .
                    docker run -d -p ${PORT}:80 ${APP_NAME}
                    '''
                }
            }
        }

        stage('Notification') {
            steps {
                echo 'Sending notification...'
                // Include your notification steps here, if applicable.
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}
