pipeline {
    agent any

    tools {
        jdk 'JAVA_HOME'
        maven 'M2_HOME'
    }

    triggers {
        githubPush()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Unit Tests') {
            steps {
                dir('backend') {
                    sh 'mvn test'
                }
            }
        }
        stage('Build Deliverable') {
            steps {
                dir('backend') {
                    sh 'mvn package -DskipTests'
                    sh 'ls -lh target/*.jar'
                }
            }
        }
    }

    post {
        failure {
            mail to: 'landoulsinourane976@gmail.com',
                 subject: "Echec du build Jenkins : ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "La pipeline a echoue lors du build #${env.BUILD_NUMBER}.\nConsulte les logs ici : ${env.BUILD_URL}"
        }
    }
}
