pipeline {
    agent any
    tools {
      maven 'Maven-3.9.5'
    }
    stages {
        stage('Source') {
            steps {
                git branch: 'main',
                    changelog: false,
                    poll: false,
                    url: 'https://github.com/hovnaz/jenkins-java-pipeline.git'
            }
        }
        stage('Clean') {
            steps {
                sh 'mvn clean'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Package') {
            steps {
                sh 'mvn package -DskipTests'
            }
        }
    }
    post {
        always {
            junit allowEmptyResults: true,
                testResults: '**/TEST-com.learningjenkins.AppTest.xml'

            archiveArtifacts allowEmptyArchive: true,
                artifacts: '**/hello-1.0-SNAPSHOT.jar'
        }
    }
}
