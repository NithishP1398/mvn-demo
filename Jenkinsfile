pipeline {
    agent any
        parameters {
  choice choices: ['dev', 'test', 'prod'], description: 'choose the environment to deploy', name: 'envname'
}
    stages {

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
