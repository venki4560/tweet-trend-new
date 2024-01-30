pipeline {
    agent {
        node {
            label 'maven'
        }
    }
    stages {
        stage("build"){
            steps {
                 echo "----------- build started ----------"
                sh 'mvn clean deploy'
                 echo "----------- build complted ----------"
            }
        }
        stage("test"){
            steps{
                echo "----------- unit test started ----------"
                sh 'mvn surefire-report:report'
                 echo "----------- unit test Complted ----------"
            }
        }
        stage('SonarQube analysis') {
            environment {
              scannerHome = tool 'devops-sonar-scanner'
                        }
            steps{
            withSonarQubeEnv('sonarqube') { // If you have configured more than one global server connection, you can specify its name
              sh "${scannerHome}/bin/sonar-scanner"
            }
            }
  }
    }
}