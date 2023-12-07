pipeline{
    agent any
    stages{
        stage('git checkout'){
            steps{
                git credentialsId: 'ccb9af01-4414-467d-b87e-90ddb6512c57', url: 'https://github.com/coldman-47/tp7'
            }
        }
        stage('Build the app'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('Unit Test Execution') {
            steps{
                sh 'mvn test'
            }
        }
        stage('Build the docker image') {
            steps{
                sh 'docker build --tag coldman47/triang7:1.0.0 .'
            }
        }
        stage('Push the docker image') {
            steps{
                withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerHubPass')]) {
                    sh "docker login -u coldman47 -p $dockerHubPass"
                }
                sh 'docker push coldman47/triang7:1.0.0'
            }
        }
    }
    post{
	    failure{
	    emailext body: 'Ce Build $BUILD_NUMBER a échoué',
	    recipientProviders:[requestor()], subject: 'build', to:
	    'doperamo@gmail.com'
  	}
  }
}
