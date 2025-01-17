pipeline {
    agent any
    tools {
        maven 'MAVEN'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'jenkins-jenkins', url: 'https://github.com/vartak14/jenkins-pipeline-example.git']])
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh "mvn test"
            }
        }
    }

    post {
        always {
            echo 'Archiving test results...'
            junit(
                allowEmptyResults: true,
                testResults: '**/target/surefire-reports/*.xml'
            )
        }
    }
}
