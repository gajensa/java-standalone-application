pipeline {
    agent any

    tools {
        jdk 'JDK21'
        maven 'Maven3'
    }

    stages {
        stage('Checkout') {
            // write your logic here
            steps {
                git branch: 'main',
                    url: 'https://github.com/gajensa/java-standalone-application.git'
            }
        }
        stage('Build') {
            // write your logic here
            steps {
                echo 'Building....'
                bat 'mvn clean install'
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
        stage('Deploy') {
            // write your logic here
            steps {
                bat 'java -cp target/java-standalone-application-1.0-SNAPSHOT.jar com.expertszen.App'
            }
        }
        post {
            success {
                script {
                    echo 'Sending email for SUCCESS...'
                    emailext(
                        subject: "SUCCESS: Jenkins Job '${env.JOB_NAME} [#${env.BUILD_NUMBER}]'",
                        body: """
                            The Jenkins job '${env.JOB_NAME}' has completed successfully.

                            Build Number: ${env.BUILD_NUMBER}
                            Status: SUCCESS
                            Build URL: ${env.BUILD_URL}
                        """,
                        to: 'sangeethagajendran2000@gmail.com'
                    )
                    echo 'Email sent.'
                }
            }
        
            failure {
                script {
                    echo 'Sending email for FAILURE...'
                    emailext(
                        subject: "FAILURE: Jenkins Job '${env.JOB_NAME} [#${env.BUILD_NUMBER}]'",
                        body: """
                            The Jenkins job '${env.JOB_NAME}' has FAILED.

                            Build Number: ${env.BUILD_NUMBER}
                            Status: FAILURE
                            Check logs here: ${env.BUILD_URL}
                        """,
                        to: 'sangeethagajendran2000@gmail.com'
                    )
                    echo 'Email sent.'
                }
            }
        
            // Optional: Run cleanup logic regardless of result
            always {
                echo "Pipeline finished with status: ${currentBuild.result}"
                // Use this block for general cleanup tasks
            }
        }
    }
}

