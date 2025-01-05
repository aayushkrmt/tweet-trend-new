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
               sh 'mvn clean deploy'
            }
        }

    stage('SonarQube analysis') {
        steps {
            withSonarQubeEnv('sonarqube-server'){
            sh "${env.scannerHome}/bin/sonar-scanner"
           }
       }
   }
   }
}
