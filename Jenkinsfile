pipeline {
    agent any

    environment {
        // Define any environment variables here
        MAVEN_HOME = '/usr/local/maven'
        AWS_REGION = 'us-east-1'
        STAGING_SERVER = 'staging-server-address'
        PRODUCTION_SERVER = 'production-server-address'
        EMAIL_RECIPIENT = 'patelriken2004@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Build the code using Maven
                    echo 'Building the code...'
                    sh '${MAVEN_HOME}/bin/mvn clean package'
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                script {
                    // Run unit tests and integration tests
                    echo 'Running unit and integration tests...'
                    sh '${MAVEN_HOME}/bin/mvn test'
                }
            }
        }

        stage('Code Analysis') {
            steps {
                script {
                    // Perform code analysis using SonarQube
                    echo 'Analyzing code with SonarQube...'
                    sh 'sonar-scanner'
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    // Perform security scan using OWASP Dependency-Check
                    echo 'Scanning for security vulnerabilities...'
                    sh 'dependency-check --project YourProject --scan . --format HTML --out dependency-check-report.html'
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                script {
                    // Deploy the application to a staging server using AWS CLI
                    echo 'Deploying to staging server...'
                    sh 'aws deploy create-deployment --application-name YourApp --deployment-group-name YourStagingGroup --s3-location bucket=your-bucket,key=your-key,bundleType=zip --region ${AWS_REGION}'
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                script {
                    // Run integration tests on the staging environment
                    echo 'Running integration tests on staging...'
                    sh '${MAVEN_HOME}/bin/mvn verify'
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                script {
                    // Deploy the application to production server using AWS CLI
                    echo 'Deploying to production server...'
                    sh 'aws deploy create-deployment --application-name YourApp --deployment-group-name YourProductionGroup --s3-location bucket=your-bucket,key=your-key,bundleType=zip --region ${AWS_REGION}'
                }
            }
        }
    }

    post {
        success {
            emailext to:  'patelriken2004@gmail.com',
                     subject: "Build Success: ${env.JOB_NAME}",
                     body: "The build was successful. Check the details in Jenkins.",
                     attachmentsPattern: '**/target/*.jar'
        }
        failure {
            emailext to: 'patelriken2004@gmail.com',
                     subject: "Build Failed: ${env.JOB_NAME}",
                     body: "The build failed. Please check the logs for details.",
                     attachmentsPattern: '**/target/*.jar'
        }
        unstable {
            emailext to: 'patelriken2004@gmail.com',
                     subject: "Build Unstable: ${env.JOB_NAME}",
                     body: "The build is unstable. Please review the details.",
                     attachmentsPattern: '**/target/*.jar'
        }
    }
}

