pipeline {
    agent any

    tools {
        maven 'Maven_3.8.8' // configure in Jenkins tools
        jdk 'JDK17'         // configure in Jenkins tools
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/tonmoym83/DemoKubernetes.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }


        stage('Docker Build') {
            steps {
                script {
                    docker.build("springboot-app:latest")
                }
            }
        }

        stage('Deploy to Docker Desktop') {
            steps {
                script {
                    docker.image("springboot-app:latest").run("-p 8080:8080")
                }
            }
        }
    }
}
