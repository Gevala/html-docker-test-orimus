
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Example build command
                sh 'docker build --no-cache -t jenkinsimage  .'
            }
        }
        stage('push') {
             steps {
                echo 'Running push...'
                sh 'docker tag jenkinsimage gevala/jenkinsimage:${BUILD_ID}'
                sh 'docker login -u="gevala" -p="675955161-Dcg"'
                sh 'docker push gevala/jenkinsimage:${BUILD_ID} '
                
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                
               sh 'ssh -o StrictHostKeyChecking=no -i "../My_Key1.pem" ec2-user@ec2-3-121-116-156.eu-central-1.compute.amazonaws.com -t "docker ps -aq | xargs docker rm -f; docker run -p 80:80 -d gevala/jenkinsimage:${BUILD_ID}"'
                
            }
        }
    }
}
