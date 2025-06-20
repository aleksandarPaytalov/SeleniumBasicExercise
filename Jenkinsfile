pipeline {
    agent any
    
    stages {
        stage('Checkout the repository') {
            steps {
                checkout scm
            }
        }
        
        stage('Restore application') {
            steps {
                bat 'dotnet restore'
            }
        }
        
        stage('Build project') {
            steps {
                bat 'dotnet build'
            }
        }
        
        stage('Test running') {
            parallel {
                stage('Run tests Project1') {
                    steps {
                        bat 'dotnet test TestProject1 --no-build --verbosity normal'
                    }
                }

                stage('Run tests Project2') {
                    steps {
                        bat 'dotnet test TestProject2 --no-build --verbosity normal'
                    }
                }

                stage('Run tests Project3') {
                    steps {
                        bat 'dotnet test TestProject3 --no-build --verbosity normal'
                    }
                }
            }
        }
    }
    
    post {
        always {
            // Clean workspace after build
            cleanWs()
        }
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
