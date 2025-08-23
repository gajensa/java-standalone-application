pipeline {
    agent any

    tools {
        jdk 'JDK21'
        maven 'Maven3'
    }

    stages {
//         stage('Checkout') {
//             // write your logic here
//             steps {
//                 git branch: 'main',
//                     url: 'https://github.com/gajensa/java-standalone-application.git'
//             }
//         }
        stage('Build') {
            // write your logic here
            steps {
                echo 'Building....'
                bat '"C:/apache-maven-3.9.9/bin/mvn" clean install'
            }
        }
        stage('Deploy') {
            // write your logic here
            steps {
                bat 'java -cp target/java-standalone-application-1.0-SNAPSHOT.jar com.expertszen.App'
            }
        }
        stage('Test') {
            // write your logic here
            steps {
                bat 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
    }
}
