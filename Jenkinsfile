pipeline {
    agent any

     tools {
        maven 'maven'
    }

    stages {
        stage('git checkout') {
            steps {
                git credentialsId: 'ec8151e0-6d82-411d-a06d-07e4b50db170',url:'https://github.com/Oumar26/TP7_DEVOPS.git'
            }
        }

        stage('Build the application'){
            steps{
                bat 'cd projetSB/spring-boot-app && mvn clean package'
            }
        }

        stage("Test Application"){
           steps {
                 bat "cd projetSB/spring-boot-app && mvn test"
               }
       }

       stage('Build the docker image'){

        steps {
          bat 'cd projetSB/spring-boot-app && docker build -t oumar22/tp7devops:1.0.0 .'
        }

       }

        stage('Push the docker image'){

        steps{
            withCredentials([string(credentialsId: 'dockerhubpass', variable:'dockerHubPass')]) {
                bat "docker login -u oumar22 -p $dockerHubPass"
            }

            bat 'docker push oumar22/tp7devops:1.0.0'

            }

        }




    }

}