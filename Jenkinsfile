pipeline{
    agent any

    environment{
        IMAGE_NAME = 'react-vite-app'
        CONTAINER_NAME = "vite-react-app0" 
    }

    stages {
        stage('Git checkout'){
            steps{

                git branch:'main', url:'https://github.com/sukhdeep07civil/react-jenkins-demo.git'
            }
        }

        stage('Build docker image'){
            steps{
                bat '''
                docker build -t %IMAGE_NAME% .
                '''
            }
        }
        stage('remove old container'){
            steps{
                bat '''
                    docker rm -f %CONTAINER_NAME || exit 0
                '''
            }
        }

        stage('run docker container'){
            steps{
                bat '''
                    docker run -d -p 5173:80 --name %CONTAINER_NAME %IMAGE_NAME%
                '''
            }
        }
    }

        post {
            success{
                echo 'Deployment successful 🚀'
            }

            failure{
                echo 'Deployment failed ❌'
            }
        }

}