pipeline {
    agent any

    stages {
        stage('Sonarqube_Test') {
            steps {
                def scannerHome = tool 'SonarQubeScanner-4.7.0'
                withSonarQubeEnv('sonarqube-8.9') {
                    sh "${scannerHome}/bin/sonar-scanner"
            }
        }
        stage('Deploy_to_AWS_S3') {
            steps {
                withCredentials([string(credentialsId: 'AWS_ACCESS_KEY_ID', variable: 'AWS_ACCESS_KEY_ID')]) { 
            
                withCredentials([string(credentialsId: 'AWS_SECRET_ACCESS_KEY', variable: 'AWS_SECRET_ACCESS_KEY')]) { 
              sh "export  AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID}"
              sh "export  AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY}"
              sh 'aws s3 cp public/index.html s3://webstatic-s3'
              sh 'aws s3 cp public/error.html s3://webstatic-s3'
                            }
            }
            }
        }
        stage('Backup_db_to_AWS_S3') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
