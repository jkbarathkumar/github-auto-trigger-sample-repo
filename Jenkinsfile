pipeline {
    agent any
    
    environment {
        GITHUB_TOKEN = credentials('GitHub_PAT') // Use your stored GitHub PAT credentials ID
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Checkout the code from repo-A
                git branch: 'main', url: 'https://github.com/jkbarathkumar/github-auto-trigger-sample-repo.git'
            }
        }
        
        stage('Deploy to GitHub Pages') {
            steps {
                // Remove the existing directory if it exists
                sh 'rm -rf auto-trigger-learning'

                // Clone repo-B where GitHub Pages is hosted
                sh 'git clone https://github.com/jkbarathkumar/auto-trigger-learning.git'

                // Copy the relevant files to repo-B (exclude the repo itself)
                sh 'cp -r Jenkinsfile index.html script.js style.css auto-trigger-learning/'

                // Configure Git identity for Jenkins user
                dir('auto-trigger-learning') {
                    sh 'git config user.name "jkbarathkumar"'
                    sh 'git config user.email "jkbarathkumar@gmail.com"'

                    // Commit and push the changes to repo-B
                    sh 'git add .'
                    sh 'git commit -m "Deploy updated code"'
                    sh 'git push https://$GITHUB_TOKEN@github.com/jkbarathkumar/auto-trigger-learning.git'
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
