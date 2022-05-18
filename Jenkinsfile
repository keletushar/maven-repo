pipeline {
    agent any

    stages {
        stage('Checkout-git') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'devopsdeepdive2', url: 'https://github.com/devopsdeepdive/maven-web-project.git']]])
            }
        }
         stage('Build') {
            steps {
                sh 'mvn validate'
        }
    }
        stage('commit') {
            steps {
                sh 'mvn commit'
        }
    }
        stage('package') {
            steps {
                sh 'mvn clean package'
        }
    }
     /*  stage('Test') {
            steps {
                sh 'mvn test'
        }
    } */
         stage('Deploy') {
            steps {
                sh 'mvn install tomcat7:deploy'
        }
    }
     stage('Notification') {
            steps {
                slackSend channel: '#pipeline-jobs', color: 'good', iconEmoji: ':with:grin:', message: 'Build is succesful and deployed', tokenCredentialId: 'slack'
        }
    }
}
}
