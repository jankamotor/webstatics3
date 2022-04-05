pipeline {
      agent any
stages{
      stage('deploy to S3'){
          steps{
              sh "export  AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID}"
              sh "export  AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY}"
              sh 'aws s3 cp public/index.html s3://webstatic-s3'
              sh 'aws s3 api put-object-acl --bucket webstatic-s3 --key index.html --acl public-read'
              sh 'aws s3 cp public/error.html s3://webstatic-s3'
              sh 'aws s3 api put-object-acl --bucket webstatic-s3 --key error.html --acl public-read'
          }
      }
  }
}
