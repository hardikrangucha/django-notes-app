@Library("Shared") _
pipeline {
    agent { label 'vinod' }

    stages {
        stage("Hello"){
            steps{
                script{
                    hello()
                }
            }
        }
        stage('Checkout Code') {
            steps {
                script{
                    clone("https://github.com/hardikrangucha/django-notes-app.git","main")
                }
            }
        }

        stage('Build') {
            steps {
                script{
                    docker_build("notes-app","latest","hardikrangucha")
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script{
                    docker_push("notes-app","latest","hardikrangucha")
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                sh "docker compose down && docker compose up -d"
            }
        }
    }
}
