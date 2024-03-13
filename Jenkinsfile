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
                    # Identify and stop any containers using the image my-web-page
                    CONTAINER_ID=$(docker ps -q --filter "ancestor=my-web-page")
                    if [ ! -z "$CONTAINER_ID" ]; then
                      echo "Stopping and removing existing my-web-page containers..."
                      docker stop $CONTAINER_ID
                      docker rm $CONTAINER_ID
                    fi

                    # Identify and stop any containers using port 8001
                    PORT_CONTAINER_ID=$(docker ps -q --filter "expose=8001")
                    if [ ! -z "$PORT_CONTAINER_ID" ]; then
                      echo "Stopping and removing any container using port 8001..."
                      docker stop $PORT_CONTAINER_ID
                      docker rm $PORT_CONTAINER_ID
                    fi

                    # Create/Update the Dockerfile
                    echo 'FROM nginx:alpine' > Dockerfile
                    echo 'COPY index.html /usr/share/nginx/html/index.html' >> Dockerfile

                    # Build the Docker image
                    docker build -t my-web-page .

                    # Attempt to run a new container from the Docker image
                    docker run -d -p 8001:80 my-web-page
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
