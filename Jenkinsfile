pipeline {
    agent {
        node {
            label 'maven'
        }
    }
    
    environment {
        PATH = "/opt/apache-maven-3.9.11/bin:$PATH"
    }

    stages {
        stage('Clone-Code') {
            steps {
                git branch: 'main', url: 'https://github.com/vivek9325/tweet-ttrend.git'
            }
        }
        
        stage('Build')
        {
            steps {
                sh 'mvn clean deploy'
            }
        }

        stage('SonarQube-Scan') {
            environment{
                scannerHome = tool 'sonar-scanner'
            }
            steps {
                withSonarQubeEnv('sonar') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
    }
}
