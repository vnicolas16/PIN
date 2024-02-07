pipeline {
  agent any

  options {
    timeout(time: 2, unit: 'MINUTES')
  }

  environment {
    ARTIFACT_ID = "elbuo8/webapp:${env.BUILD_NUMBER}"
    DOCKER_HUB_LOGIN = credentials('docker')
    REGISTRY = "vnicolas16"
  }
   stages {
    stage('Building image') {
      steps{
          sh 'docker build -t testapp . '
        }
    }
  
  
    stage('Run tests') {
      steps {
        sh "docker run testapp npm test"
      }
    }
    stage('Deploy Image to Hub') {
      steps{
        sh '''
        docker login --username=$DOCKER_HUB_LOGIN_USR --password=$DOCKER_HUB_LOGIN_PSW
        docker tag testapp $REGISTRY/testapp:v1
        docker push $REGISTRY/testapp:v1   
        '''
        }
      }
    }
}


    
  

