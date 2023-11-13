pipeline{
    agent any

    environment {
        DOCKER_HUB_USERNAME = 'jihen546'
        DOCKER_IMAGE_NAME = 'mynodeapp'
        TAG = 'latest'
        K8S_DEPLOYMENT_NAME = 'nodejs-app-deployment'
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
                    echo "__Image built__"
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
                    // Use the credentials by their ID
                    withCredentials([usernamePassword(credentialsId: 'dockerhub_id',usernameVariable: 'DOCKER_HUB_USERNAME', passwordVariable: 'DOCKER_HUB_PASSWORD')]) {
                        sh "docker login -u $DOCKER_HUB_USERNAME -p $DOCKER_HUB_PASSWORD"
                        sh "docker tag ${DOCKER_IMAGE_NAME}:${TAG} ${DOCKER_HUB_USERNAME}/${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_NAME}"
                        sh "docker push ${DOCKER_HUB_USERNAME}/${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_NAME}"
                    }
                    echo "__Image pushed__"
                }
            }
        }

        stage("Deploy to Kubernetes") {
            steps {
                script {
                    echo "======== Deploying to Kubernetes ========"
                    def kubectlPath = "C:\\ProgramData\chocolatey\bin"
                    bat "${kubectlPath} kubectl version"
                    // sh "kubectl version"
                    // sh "kubectl create deployement ${K8S_DEPLOYMENT_NAME} --image=${DOCKER_HUB_USERNAME}/${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_NAME}"
                    // sh "kubectl set image deployment/${K8S_DEPLOYMENT_NAME} ${K8S_DEPLOYMENT_NAME}=${DOCKER_HUB_USERNAME}/${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_NAME} -n ${K8S_NAMESPACE}"
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
