pipeline {
    agent any

    tools {
        maven 'Maven3'   // Must match the name in Manage Jenkins → Tools
        jdk 'JDK21'      // Must match the name in Manage Jenkins → Tools
    }

    stages {

        stage('Clone Code') {
            steps {
                echo 'Cloning repository from GitHub...'
                git branch: 'master',
                    url: 'https://github.com/Aditya-cts/Google-Search-Automation.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Compiling the project...'
                bat 'mvn compile'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running Selenium TestNG suite...'
                bat 'mvn clean test'
            }
        }

        stage('Publish Reports') {
            steps {
                echo 'Publishing TestNG results...'
            }
            post {
                always {
		    testNG '**/target/surefire-reports/testng-results.xml'
		}
            }
        }

    }

    post {
        success {
            echo '✅ Build Passed! All tests successful.'
        }
        failure {
            echo '❌ Build Failed! Check console output.'
        }
    }
}
