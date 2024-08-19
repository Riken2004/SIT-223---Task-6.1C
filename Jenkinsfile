pipeline {
    agent any
    
    environment {
        MAVEN_HOME = '/path/to/your/maven'
        JAVA_HOME = '/path/to/your/java'
        PATH = "${MAVEN_HOME}/bin:${JAVA_HOME}/bin:${env.PATH}"
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
                    echo "Building the code with Maven..."
                    bat "${MAVEN_HOME}/bin/mvn clean install"
                }
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo "Running Unit and Integration Tests..."
                    bat "${MAVEN_HOME}/bin/mvn test"
                }
            }
        }
        
        stage('Code Analysis with Checkstyle') {
            steps {
                script {
                    echo "Running Checkstyle..."
                    bat "${MAVEN_HOME}/bin/mvn checkstyle:check"
                }
            }
        }

        stage('Code Analysis with PMD') {
            steps {
                script {
                    echo "Running PMD..."
                    bat "${MAVEN_HOME}/bin/mvn pmd:check"
                }
            }
        }
        
        stage('Code Analysis with SpotBugs') {
            steps {
                script {
                    echo "Running SpotBugs..."
                    bat "${MAVEN_HOME}/bin/mvn spotbugs:check"
                }
            }
        }
        
        stage('Security Scan with OWASP Dependency Check') {
            steps {
                script {
                    echo "Running OWASP Dependency Check..."
                    bat "${MAVEN_HOME}/bin/mvn org.owasp:dependency-check-maven:check"
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                script {
                    echo "Deploying to Staging..."
                    bat "deploy.bat staging"  // Replace with your actual deployment command or script
                }
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo "Running Integration Tests on Staging..."
                    bat "run-staging-tests.bat"  // Replace with your actual testing command or script
                }
            }
        }
        
        stage('Deploy to Production') {
            steps {
                script {
                    echo "Deploying to Production..."
                    bat "deploy.bat production"  // Replace with your actual deployment command or script
                }
            }
        }
    }
    
    post {
        always {
            emailext (
                subject: "Jenkins Pipeline Build #${BUILD_NUMBER} - ${BUILD_STATUS}",
                body: """Build #${BUILD_NUMBER} has finished with status: ${BUILD_STATUS}
                         Check console output at ${BUILD_URL} to view the results.""",
                to: 'your-email@example.com'
            )
        }
    }
}
