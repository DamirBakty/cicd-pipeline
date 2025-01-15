pipeline {
  agent any
  stages {
    stage('Git Checkout') {
      steps {
        git(url: 'https://github.com/DamirBakty/cicd-pipeline', branch: 'main')
      }
    }

    stage('Application Build') {
      steps {
        sh 'bash scripts/build.sh'
      }
    }

    stage('Tests') {
      steps {
        sh 'bash scripts/test.sh'
      }
    }

    stage('Docker Image Build') {
      steps {
        script {
          sh """
          docker build -t jenkins_image:latest .
          docker tag jenkins_image:latest ultimate1465/jenkins_image:latest
          """
        }
      }
    }

    stage('Docker Image Push') {
      steps {
        script {
            sh """
            echo password | docker login -u ultimate1465 --password-stdin
            docker push ultimate1465/jenkins_image:latest
            """
        }
      }
    }
  }
}
