pipeline {
    agent any

    environment {
        MAVEN_HOME = 'C:\\Program Files\\apache-maven-3.9.9'
        JAVA_HOME = 'C:\\Program Files\\Common Files\\Oracle\\Java\\javapath\\java.exe'
        PATH = "${env.MAVEN_HOME}\\bin;${env.JAVA_HOME}\\bin;${env.PATH}"
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
                    bat "${env.MAVEN_HOME}\\bin\\mvn clean install"
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo "Running Unit and Integration Tests..."
                    bat "${env.MAVEN_HOME}\\bin\\mvn test"
                }
            }
        }

        stage('Code Analysis') {
            steps {
                script {
                    echo "Performing Code Analysis with SpotBugs..."
                    bat "${env.MAVEN_HOME}\\bin\\mvn spotbugs:check"
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    echo "Performing Security Scan with OWASP Dependency Check..."
                    bat "${env.MAVEN_HOME}\\bin\\mvn org.owasp:dependency-check-maven:check"
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                script {
                    echo "Deploying to Staging..."
                    bat "deploy-staging.bat"
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo "Running Integration Tests on Staging..."
                    bat "run-staging-tests.bat"
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                script {
                    echo "Deploying to Production..."
                    bat "deploy-production.bat"
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
                to: 'patelriken2004@gmail.com'
            )
        }
    }
}



