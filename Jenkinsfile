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
    always {
        script {
            try {
                echo "📧 Attempting to send email..."
                emailext(
                    to: 'saravind@sirahu.com',
                    subject: "🔔 Build ${currentBuild.number} Status: ${currentBuild.currentResult}",
                    body: "Build ${currentBuild.number} completed with status: ${currentBuild.currentResult}. Check details here: ${env.BUILD_URL}",
                    attachLog: true
                )
                echo "✅ Email sent successfully."
            } catch (Exception e) {
                echo "❌ Email sending failed: ${e.getMessage()}"
            }
        }
    }
}

}
