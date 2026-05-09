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

    }
}
