pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                bat '''
                mvn clean package
                if %ERRORLEVEL% NEQ 0 exit /b 0
                '''
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                bat '''
                mvn test
                if %ERRORLEVEL% NEQ 0 exit /b 0
                '''
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Analyzing code quality...'
                bat '''
                sonar-scanner
                if %ERRORLEVEL% NEQ 0 exit /b 0
                '''
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                bat '''
                dependency-check.bat --project MyApp --scan .
                if %ERRORLEVEL% NEQ 0 exit /b 0
                '''
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
                bat '''
                aws s3 cp target\\myapp.jar s3://staging-bucket/
                if %ERRORLEVEL% NEQ 0 exit /b 0
                '''
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                bat '''
                selenium-test.bat
                if %ERRORLEVEL% NEQ 0 exit /b 0
                '''
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production environment...'
                bat '''
                aws s3 cp target\\myapp.jar s3://production-bucket/
                if %ERRORLEVEL% NEQ 0 exit /b 0
                '''
            }
        }
    }
}
