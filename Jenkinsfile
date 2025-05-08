pipeline {
    // Optionally restrict the build to Windows nodes:
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Tool: Maven – ensure Maven is installed and added to PATH
                bat 'mvn clean package'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                bat 'mvn test'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Analyzing code quality...'
                // Tool: SonarQube – ensure sonar-scanner is available for Windows
                bat 'sonar-scanner'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                // Tool: OWASP Dependency-Check – use the Windows batch file (dependency-check.bat) if available
                bat 'dependency-check.bat --project MyApp --scan .'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
                // Tool: AWS CLI – note the use of backslashes for file paths if necessary
                bat 'aws s3 cp target\\myapp.jar s3://staging-bucket/'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Tool: Selenium / API testing – ensure you have a Windows-compatible script (e.g., selenium-test.bat)
                bat 'selenium-test.bat'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production environment...'
                bat 'aws s3 cp target\\myapp.jar s3://production-bucket/'
            }
        }
    }
}
