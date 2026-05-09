pipeline {

    agent any

    tools {
        jdk 'JAVA_HOME'
        maven 'M2_HOME'
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/Miku172002/webapp.git'
            }
        }

        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Rename WAR') {
            steps {
                sh 'mv target/*.war target/myweb.war'
            }
        }

        stage('Deploy') {
            steps {

                sshagent(['tomcatnew']) {

                    sh """
                    scp -o StrictHostKeyChecking=no target/myweb.war ec2-user@16.171.115.17:/home/ec2-user/tomcat10/webapps/

                    ssh -o StrictHostKeyChecking=no ec2-user@16.171.115.17 /home/ec2-user/tomcat10/bin/shutdown.sh

                    ssh -o StrictHostKeyChecking=no ec2-user@16.171.115.17 /home/ec2-user/tomcat10/bin/startup.sh
                    """
                }
            }
        }

    }
}
