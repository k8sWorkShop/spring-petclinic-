pipeline {
    agent  {label 'k8s-workshop'}
    //  triggers {
    //      pollSCM('* * * * *')
    // }

    stages {
        stage ('git checkout') {
            steps {
                git url: 'https://github.com/k8sWorkShop/spring-petclinic-.git', branch: 'develop'
            }
        }
        stage ('build docker image') {
            steps {
                sh 'docker image build -t petclinic:latest .'
                
            }
        }
        stage ('docker tag/rename image'){
            steps{
                sh 'docker tag petclinic:latest practices.jfrog.io/ajay-docker-local/petclinic:v1.0 '
            }
        }
        stage ('push image to jfrog artifactory and scan image') {
            steps {
                sh 'docker image push practices.jfrog.io/ajay-docker-local/petclinic:v1.0'
            }
        }
        stage ('deploy') {
            steps {
                sh 'kubectl apply -f k8s/'
            }
        }
    }
}