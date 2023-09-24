pipeline {
    agent any
    stages {
        stage ('vcs') {
            steps {
                git url 'https://github.com/WorkshopsByKhaja/petclinic.git', branch: 'develop'
            }
        }
        stage ('build docker image') {
            steps {
                sh 'docker image build -t qt1234.jfrog.io/workshop-docker-local/petclinic:latest .'
            }
        }
        stage ('send to artifactory and scan') {
            steps {
                sh 'docker image push qt1234.jfrog.io/workshop-docker-local/petclinic:latest'
            }
        }
        stage ('deploy') {
            steps {
                sh 'kubectl apply -f '
            }
        }
    }
}