pipeline {
    agent any
    parameters {
  choice choices: ['Dev', 'test', 'prod'], name: 'Choice'
}
       stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', credentialsId: '7b5ba1e3-03c8-43ee-835c-d2e6e81dcf73', url: 'https://github.com/NithishP1398/mvn-demo.git'
            }
        }
        stage('maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Tomcat Deployment') {
            steps {
                sshagent(['Deployment']) {
            sh "scp -o StrictHostKeyChecking=no target/mvn-demo.jar ec2-user@172.31.0.247:/opt/tomcat9/webapps"
            sh "ssh ec2-user@172.31.0.247 /opt/tomcat9/bin/shutdown.sh"
            sh "ssh ec2-user@172.31.0.247 /opt/tomcat9/bin/startup.sh"
}
                
            }
        }
    }
}
