pipeline {
    agent any
    tools {
            jdk 'myjava'
            maven 'mymaven'
    }
    
    options {
            buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '1', numToKeepStr: '1')
    }

    stages {
        stage('Git Checkout') {
            steps {
                echo 'Git Version and Brach Check'
                checkout changelog: false, poll: false, scm: scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/adevopstech/maven-java-sample.git']])
            }
        }
        stage('Maven Validate') {
            steps {
                echo 'Maven Validate the code'
                sh 'mvn validate'
            }
        }
        stage('Maven Compile') {
            steps {
                echo 'Maven Compile the code'
                sh 'mvn compile'
            }
        }
        stage('Maven Test') {
            steps {
                echo 'Maven Test the code'
                sh 'mvn test'
            }
        }
        stage('Deploy Package') {
            steps {
                echo 'Maven Package Deploy'
                sh 'mvn package'
            }
        }
    }
}