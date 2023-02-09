pipeline{
    agent none
    environment {
        DOCKERHUB_CREDENTIALS=credentials('d89a308f-32e9-466c-a4f0-99a6750dd8fd')
    }
    
    stages{
        stage('Hello'){
            agent{ 
                label 'kub-master'
            }
            steps{
                echo 'Hello World'
            }
        }
        stage('git'){
            agent{ 
                label 'kub-master'
            }

            steps{

                git'https://github.com/niveditapa21/website1.git'
            }
        }
        stage('docker') {
            agent { 
                label 'kub-master'
            }

            steps {

                sh 'sudo docker build https://github.com/niveditapa21/website1/Jenkinsfile -t nivedita21/kube-image1'
                sh 'sudo echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                sh 'sudo docker push nivedita21/kube-image1'

            }
        }
        stage('Kuberneets') {
            agent { 
                label 'kub-master'
            }

            steps {

                sh 'sudo kubectl create -f deploy.yml'
                sh 'sudo kubectl create -f svc.yml'
            }
        }        
        
    }
}
