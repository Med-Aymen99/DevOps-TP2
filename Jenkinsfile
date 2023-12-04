pipeline{
    agent any

    environment {
        DOCKER_HUB_USERNAME = 'jihen546'
        DOCKER_IMAGE_NAME = 'mynodeapp'
        TAG = 'latest'
    }

    stages{

        stage("Pull from GitHub") {
            steps {
                echo "__Pulling from GitHub__"
                git url: 'https://github.com/Med-Aymen99/DevOps-TP2.git', branch: 'master'
                sh "ls -ltr"
            }
        }

    //    build de l'image
        stage("Build Docker Image"){
            steps {                
                script {
                    echo "__Building Docker Image__"
                    docker.build("${DOCKER_IMAGE_NAME}:${TAG}")
                    echo "__Image built__"
                }            
            }
        }
        
        stage("Push Docker Image") {
            steps {
                script {
                    echo "__Pushing Docker Image__"
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_id') {
                        docker.image("${DOCKER_HUB_USERNAME}/${DOCKER_IMAGE_NAME}:${TAG}").push()
                        docker.image("${DOCKER_HUB_USERNAME}/${DOCKER_IMAGE_NAME}:${TAG}").tag("${DOCKER_HUB_USERNAME}/${DOCKER_IMAGE_NAME}:${TAG}", "registry.hub.docker.com/${DOCKER_HUB_USERNAME}/${DOCKER_IMAGE_NAME}:${TAG}")
                    }
                    echo "__Image pushed__"
                }
            }
        }
  
    }
    
    post{
        success{
            echo "======== Setting up infra executed successfully ========"
        }
        failure{
            echo "======== Setting up infra execution failed ========"
        }
    }
             
}
