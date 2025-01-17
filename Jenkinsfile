pipeline {
agent any
tools {
    maven '3.8.7'
}

stages {
    stage('Build') {
        steps {
            echo 'Hello World'
            checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'jenkins-jenkins ', url: 'https://github.com/vartak14/jenkins-pipeline-example.git']])
            sh "mvn -Dmaven.test.failure.ignore=true clean package"
        }
    }
}
post {
    always {
        junit(
            allowEmptyResults:true,
            testResults: 'test-reports/.xml'
            )
        }
    }
}
