pipeline {
    agent any

    stages {
        stage('Cleanup') {
            steps {
                sh ''' 
                docker stop webapp-container || true
                docker rm webapp-container || true
                docker rmi webapp-image ||true
                '''
            }
        }

        stage('Build Image') {
            steps {
                sh ''' 
                cd Task1
                docker build -t webapp-image .
                '''
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker run -d -p 80:80 --name webapp-container webapp-image
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                # Wait for container to be fully up
                sleep 5
                # Test if the webapp is responding 
                curl localhost:80 || echo "Website not responding"
                '''
            }
        }
    }
}