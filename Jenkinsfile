def registry =  'https://aayushish.jfrog.io/'
def imageName = 'aayushish.jfrog.io/valaxy-docker-local/ttrend'
def version = '2.1.2'

pipeline {
    agent {
         node {
             label 'maven'
         }
    }
environment {
    PATH = "/opt/apache-maven-3.9.9/bin:$PATH"
    scannerHome = tool 'valaxy-sonar-scanner'
}
    stages {
        stage('Build') {
            steps {
               sh 'mvn clean deploy -Dmaven.test.skip=true'
            }
        }
        stage('Test'){
            steps {
                sh 'mvn surefire-report:report'
            }    
       }
   stage('SonarQube analysis') {
    environment {
      scannerHome = tool 'valaxy-sonar-scanner'
    }
    steps{
    withSonarQubeEnv('valaxy-sonarqube-server') { // If you have configured more than one global server connection, you can specify its name
      sh "${scannerHome}/bin/sonar-scanner"
    }
    }
  }      
      
 }
}
