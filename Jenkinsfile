pipeline {
    agent {
        node {
        label 'maven-build-server'
        }
    }
    tools {
        maven 'maven-3.9.6'
    }
  stages {
    stage('Packaging') {
        steps {
            echo 'Packaging..'
            sh 'mvn clean package'
        }
    stage('Copying war file') {
        steps {
            echo 'Copying war file..'
            sh 'mv target/*.war .'
        }
    stage('cleanup') {
      steps {
        sh 'docker container stop devops-web-project-server'
        sh 'docker container rm devops-web-project-server'
      }
    }
    stage('build image') {
      steps {
        sh 'docker build -t jogucha/devops-web-project:1 .'
      }
    }
    stage('run container') {
      steps {
        sh 'docker run -d --name devops-web-project-server -p 8081:8080 jogucha/devops-web-project:v1'
      }
    }
  }
}