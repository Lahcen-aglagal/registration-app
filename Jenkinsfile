pipeline {
    agent { label 'Jenkins-Agent' }
    tools {
        jdk 'Java17'
        maven 'Maven3'
    }
    environment {
        APP_NAME = "register-app-pipeline"
        RELEASE = "1.0.0"
        DOCKER_USER = "lahcenaglagal"
        DOCKER_PASS = "dockerhub"
        IMAGE_NAME = "${DOCKER_USER}/${APP_NAME}" // Correction ici.
    }
    stages {
        stage("Cleanup Workspace") {
            steps {
                cleanWs()
            }
        }
        stage("Checkout from SCM") {
            steps {
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/Lahcen-aglagal/registration-app.git'
            }
        }
        stage("Build Application") {
            steps {
                sh "mvn clean package"
            }
        }
        stage("Test Application") {
            steps {
                sh "mvn test"
            }
        }
        stage("Build and Push Docker Image") {
            steps {
                script {
                    // Construire l'image Docker
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_PASS) {
                        def docker_image = docker.build("${IMAGE_NAME}:${RELEASE}-${env.BUILD_NUMBER}")
                        
                        // Pousser les images Docker
                        docker_image.push("${RELEASE}-${env.BUILD_NUMBER}")
                        docker_image.push("latest")
                    }
                }
            }
        }
    }
}
