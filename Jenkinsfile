pipeline {
    agent any
    tools{
        jdk "JAVA_HOME"
        maven "MAVEN_HOME"
    }
    stages {
        stage('Checkout-git') {
            steps {
checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'git-ant', url: 'https://github.com/keletushar/maven-repo.git']]])                
            }
        }
         
}
}
