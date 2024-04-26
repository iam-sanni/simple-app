pipeline {
    agent any
    tools {
      nodejs '20.7.0'
    }
    stages {
        stage('print versions') {
          steps {
            sh 'npm version'
          }
        }
        stage('codedeploy'){
          steps {
            step([$class: 'AWSCodeDeployPublisher', applicationName: 'sample-app', deploymentGroupAppspec: false, deploymentGroupName: 'sample-app', excludes: '', iamRoleArn: '', includes: 'dist/', proxyHost: '', proxyPort: 0, region: 'us-east-1', s3bucket: 'deploymasters-nodejs', s3prefix: '', subdirectory: '', versionFileName: '', waitForCompletion: false])
           }
        }
    }
}
