pipeline {
    agent any
    
    environment {
        MAVEN_HOME = 'C:\\Users\\Riken patel\\apache-maven-3.8.8-bin' // Adjust path to your Maven installation
        JAVA_HOME = 'C:\\Program Files\\Java\\jdk-11.0.11' // Adjust path to your Java installation
    }
    
    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                script {
                    echo "Building the code..."
                    bat "${MAVEN_HOME}\\bin\\mvn clean install"
                }
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo "Running Unit and Integration Tests..."
                    bat "${MAVEN_HOME}\\bin\\mvn test"
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                script {
                    echo "Performing Code Analysis..."
                    // Example: Using SonarQube for code analysis
                    // Replace with your actual command for code analysis
                    bat "${MAVEN_HOME}\\bin\\mvn sonar:sonar"
                }
            }
        }
        
        stage('Security Scan') {
            steps {
                script {
                    echo "Performing Security Scan..."
                    // Example: Using OWASP Dependency Check for security scan
                    // Replace with your actual command for security scanning
                    bat "dependency-check.bat --project JenkinsPipeline --scan ."
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                script {
                    echo "Deploying to Staging..."
                    // Example: Deploying using a custom deployment script
                    // Replace with your actual deployment command
                    bat "deploy.bat staging"
                }
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo "Running Integration Tests on Staging..."
                    // Replace with your actual commands to run tests on the staging environment
                    bat "run-staging-tests.bat"
                }
            }
        }
        
        stage('Deploy to Production') {
            steps {
                script {
                    echo "Deploying to Production..."
                    // Example: Deploying to production using a custom deployment script
                    // Replace with your actual production deployment command
                    bat "deploy.bat production"
                }
            }
        }
    }
    
    post {
        always {
            emailext (
                subject: "Jenkins Pipeline Build #${BUILD_NUMBER} - ${currentBuild.currentResult}",
                body: """Build #${BUILD_NUMBER} has finished with status: ${currentBuild.currentResult}
                         Check console output at ${BUILD_URL} to view the results.""",
                to: 'patelriken2004@gmail.com'
            )
        }
    }
}


