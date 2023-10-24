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
                echo "test1"
                git url: 'https://github.com/Med-Aymen99/DevOps-TP2.git', branch: 'master'
                sh "ls -ltr"
            }
        }

    //    build de l'image
        stage("Build Docker Image"){
            steps {                
                script {
                    echo "== executing =="
                    sh "docker build -t ${DOCKER_IMAGE_NAME}:${TAG} ."
                    echo "Building image"
                }            
            }
        }
        
        stage("Push Docker Image") {
            steps {                
                script {
                    echo "======== executing ========"
                    sh "pwd"
                    sh "ls"
                    echo "push to hub"
                    sh "docker tag ${DOCKER_IMAGE_NAME}:${TAG} ${DOCKER_HUB_USERNAME}/devopstp:${DOCKER_IMAGE_NAME}"
                    sh "docker push ${DOCKER_HUB_USERNAME}/devopstp:${DOCKER_IMAGE_NAME}"
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
