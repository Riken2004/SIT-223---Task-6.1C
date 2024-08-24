pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Build'
                echo 'Detail: Build code using automation tool which will compile and package'
                echo 'Build Automation Tool: Maven is used to conduct build automation testing !!!'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
               echo 'Stage 2: Unit and Integration Test'
                echo 'Detail: Run unit tests to ensure code operates as expected. Run integration tests to ensure components operate together as expected'
                echo 'Test Automation Tool: JUnit 5 is the testing framework used for unit testing'
                }
                post {
                    success {
                        emailext(
                            attachLog: true,
                            to: 'patelriken2004@gmail.com',
                            subject: 'Unit and Integration Test: Successful',
                            body: 'Stage 2 successfully implemented. Refer to the report.'
                        )
                    }
                    failure {
                        emailext(
                            attachLog: true,
                            to: 'patelriken2004@gmail.com',
                            subject: 'Unit and Integration Test: Failure',
                            body: 'Stage 2 unsuccessfully implemented. Refer to the report.'
                        )
                    }
                }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Code Analysis'
                echo 'Detail: Analyze code to ensure it meets industry standards'
                echo 'Code Analysis Tool: SonarQube is used for static code analysis'
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Stage 4: Security Scan'
                echo 'Detail: Perform a security scan to check for vulnerabilities'
                echo 'Security Scan Tool: OWASP Security tool is used to perform security vulnerability scans'
            }
            post {
                success {
                    emailext (
                        attachLog: true,
                        to: 'patelriken2004@gmail.com',
                        subject: 'Security Scan Test: Successful',
                        body: 'Stage 4 successfully implemented. Refer to the report.'
                    )
                }
                failure {
                    emailext(
                        attachLog: true,
                        to: 'patelriken2004@gmail.com',
                        subject: 'Security Scan Test: Failure',
                        body: 'Stage 4 unsuccessfully implemented. Refer to the report.'
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploy to Staging'
                echo 'Detail: Deploy application to staging environment (AWS EC2)'     
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Integration Tests on Staging'
                echo 'Detail: Conduct integration tests in staging environment to ensure functions as expected in a production-like environment'                
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploy to Production'
                echo 'Detail: Deploy application to production environment (AWS EC2)'
            }
        }
    }
}

