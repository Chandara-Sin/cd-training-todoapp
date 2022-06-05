pipeline{
    agent any
    stages{
        stage('Build Image'){
            steps{
                sh "docker build -t chandarasin/todoapp:latest ."
            }
        }
        stage('Login resgistry'){
            steps{
                sh "docker login -u chandarasin -p 'chandara123@$'"
            }
        }
        stage('Push Image'){
            steps{
                sh "docker push chandarasin/todoapp:latest"
            }
        }
        stage('Copy Docker Compose'){
            steps{
                sh """
                    scp -i ~/.ssh/build-server-rsa -r ./docker-compose.yml ec2-user@ec2-13-215-252-7.ap-southeast-1.compute.amazonaws.com:/home/ec2-user/todoapp/docker-compose-prod.yml
                """
            }
        }
        stage('Deploy'){
            steps{
                sh  """
                    ssh -i ~/.ssh/build-server-rsa -tt ec2-user@ec2-13-215-252-7.ap-southeast-1.compute.amazonaws.com "
                        cd todoapp
                        docker login -u chandarasin -p 'chandara123@$'
                        docker-compose -f docker-compose-prod.yml pull
                        docker-compose -f docker-compose-prod.yml up -d
                    "
                """
            }
        }
    }
}