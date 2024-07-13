pipeline {
    agent any

    tools {
        // Install the Maven version configured as "Maven 3.6.3" in the global configuration
        maven 'Maven 3.6.3'
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/Anujmonty/simple-java-app.git'

                // Run Maven on a Unix agent.
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                // Run tests
                sh 'mvn test'
            }
        }
    }

    post {
        // If Maven was able to run the tests, even if some of the test
        // failed, record the test results and archive the built artifacts.
        always {
            junit '**/target/surefire-reports/TEST-*.xml'
            archiveArtifacts 'target/*.jar'
        }
    }
}
