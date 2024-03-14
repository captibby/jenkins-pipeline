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
                    APP_NAME="my-web-page"
                    PORT="8000"

                    # Find the container ID running on the specified port and stop/remove it
                    CONTAINER_ID=$(docker ps --filter "status=running" -a | grep ":${PORT}->" | awk '{print $1}')
                    if [ ! -z "$CONTAINER_ID" ]; then
                      echo "Found container $CONTAINER_ID running on port ${PORT}, stopping and removing..."
                      docker stop $CONTAINER_ID
                      docker rm $CONTAINER_ID
                    else
                      echo "No container found running on port ${PORT}."
                    fi

                    echo 'Creating Dockerfile...'
                    echo 'FROM nginx:alpine' > Dockerfile
                    echo 'COPY index.html /usr/share/nginx/html/index.html' >> Dockerfile

                    echo 'Building Docker image...'
                    docker build -t ${APP_NAME} .

                    echo 'Running new Docker container...'
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
