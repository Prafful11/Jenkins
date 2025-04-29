pipeline {
    agent any
    environment {
        DOCKER_BUILDKIT = '1'
    }
    stages {
        stage('Prepare') {
            steps {
                cleanWs()
                dir('frontend') {
                    sh 'npm install'
                }
                dir('backend') {
                    sh 'npm install'
                }
            }
        }

        stage('Dependency Check') {
            steps {
                dependencyCheck additionalArguments: '--format XML'
            }
        }

        stage('Trivy Scan') {
            steps {
                sh 'trivy fs --scanners vuln --format table -o trivy-fs-report.html .'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }
}
