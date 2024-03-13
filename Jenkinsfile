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
                    # Check if any containers are using the target port and stop/remove them
                    CONTAINER_ID=$(docker ps -q --filter "ancestor=my-web-page")
                    if [ ! -z "$CONTAINER_ID" ]; then
                      docker stop $CONTAINER_ID
                      docker rm $CONTAINER_ID
                    fi

                    # Create/Update the Dockerfile
                    echo 'FROM nginx:alpine' > Dockerfile
                    echo 'COPY index.html /usr/share/nginx/html/index.html' >> Dockerfile

                    # Build the Docker image
                    docker build -t my-web-page .

                    # Run a new container from the Docker image
                    docker run -d -p 8002:80 my-web-page
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
