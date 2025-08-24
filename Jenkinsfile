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
        }
        stage('Deploy') {
            // write your logic here
            steps {
                bat 'java -cp target/java-standalone-application-1.0-SNAPSHOT.jar com.expertszen.App'
            }
        }    
    }
     post {
        always {
            // This runs after every build, regardless of the result.
            // Good for cleanup, archiving, and publishing reports.
            echo "Publishing test results..."
            junit 'target/surefire-reports/*.xml'
        }
        success {
            // This block only runs if the entire pipeline is successful.
            echo 'Sending SUCCESS email notification...'
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
        }
        failure {
            // This block only runs if the entire pipeline fails.
            echo 'Sending FAILURE email notification...'
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
        }
        unstable {
            // This block only runs if the pipeline finished with UNSTABLE status (e.g., test failures).
            echo 'Sending UNSTABLE email notification...'
            emailext(
                subject: "UNSTABLE: Jenkins Job '${env.JOB_NAME} [#${env.BUILD_NUMBER}]'",
                body: """
                    The Jenkins job '${env.JOB_NAME}' has finished UNSTABLE.
                    
                    Build Number: ${env.BUILD_NUMBER}
                    Status: UNSTABLE (Check test results)
                    Check logs here: ${env.BUILD_URL}
                """,
                to: 'sangeethagajendran2000@gmail.com'
            )
        }
    }
}


