pipeline {
    agent any //run this on whatever jenkins server is available
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds') //credentials for dockerhub already stored in jenkins
        IMAGE_NAME = 'Ashezzz/jenkins-pipeline' //name of the image to be built and pushed to dockerhub
    }
    stages {
        stage('Clone'){
            steps {
                echo 'Cloning the repository...' //print a message to indicate the cloning process
                checkout scm //checkout the code from the repository
              }
            }
        stage('lint'){
            steps {
                echo 'Running lint checks...' //print a message to indicate the linting process
                sh  'echo lint checks passed!' //simulate linting process
              }
            }
        stage('Test'){
                steps {
                    echo 'Running tests...' //print a message to indicate the testing process
                    sh 'echo all tests passed!' //simulate testing process
                }
            }
        stage('Build Docker Image'){
                steps {
                    echo 'Building Docker image...' //print a message to indicate the building process
                    sh "docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} ." //build the docker image with a tag that includes the build number that is automatically incremented by jenkins"
                }}
        stage('Push to Docker Hub'){
                    steps{
                        sh "echo ${DOCKERHUB_CREDENTIALS_PSW} | docker login -u ${DOCKERHUB_CREDENTIALS_USR} --password-stdin" //login to dockerhub using the credentials stored in jenkins
                        sh "docker push ${IMAGE_NAME}:${BUILD_NUMBER}" //push the docker image to dockerhub

                    }
                    }
        stage('Deploy'){
                    steps {
                        sh "docker stop jenkins-pipeline || true" //stop the running container if it exists, ignore errors if it doesn't exist
                        sh "docker rm jenkins-pipeline || true" //remove the stopped container, ignore errors if it doesn't exist
                        sh "docker run -d --name jenkins-pipeline-new -p 80:3000 ${IMAGE_NAME}:${BUILD_NUMBER}" //run the docker image as a container
                }
                }
         }   
        post {
                success {
                    echo 'Pipeline completed successfully!' //print a message to indicate the successful completion of the pipeline
                }
                failure {
                    echo 'Pipeline failed. Please check the logs for details.' //print a message to indicate the failure of the pipeline
            }
         }
     }

