pipeline {
    agent any

    stages {
        stage('Checkout-git') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'devopsdeepdive2', url: 'https://github.com/devopsdeepdive/maven-web-project.git']]])
                
            }
        }
         stage('Validate') {
            steps {
                sh 'mvn validate'
        }
                sh 'mvn compile'
        }
    }
              stage('Test') {
            steps {
                sh 'mvn test'
    }
        stage('Compile') {
            steps {
        }
    } 
        stage('package') {
            steps {
                sh 'mvn clean package'
        }
    }
 
         stage('Deploy') {
            steps {
               sshagent(['tomcat-deploy']) {
   sh "scp ssh -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/maven-pipeline/target/maven-web-application.war ubuntu@172.31.0.116:/opt/apache-tomcat-9.0.63/webapps"

}
        }
    }
   /*  stage('Notification') {
            steps {
                slackSend channel: '#pipeline-jobs', color: 'good', iconEmoji: ':with:grin:', message: 'Build is succesful and deployed', tokenCredentialId: 'slack'
        }
    } */
}
}
