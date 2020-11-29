pipeline {
  environment {
    imagename = "html-server-image"
    registryCredential = '518572'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/rajeev-raj/AB-challenge.git', branch: 'master', credentialsId: 'github-id'])

      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build imagename
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com/', '518572' ) {
            dockerImage.push("$BUILD_NUMBER")
             dockerImage.push('latest')

          }
        }
      }
    }
    stage('running docker image') {
      steps{
	sh "docker run $imagename"
        #sh "docker rmi $imagename:$BUILD_NUMBER"
         #sh "docker rmi $imagename:latest"

      }
    }
  }
}
