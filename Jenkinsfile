pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/aravind-zinnect/simple-repo3'
            }
        }

        stage('Create Artifact') {
            steps {
                script {
                    bat 'echo This is my Jenkins artifact file > my_report.txt'
                }
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'my_report.txt', fingerprint: true
            }
        }
    }

    post {
        success {
            emailext subject: "✅ Build Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                     body: "The build was successful! Check the artifacts here: ${env.BUILD_URL}/artifact/",
                     to: 'your-email@gmail.com'
        }
        failure {
            emailext subject: "❌ Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                     body: "The build failed. Check the logs here: ${env.BUILD_URL}/console",
                     to: 'your-email@gmail.com'
        }
    }
}
