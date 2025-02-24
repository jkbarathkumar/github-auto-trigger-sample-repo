pipeline {
    agent any
    
    environment {
        GITHUB_TOKEN = credentials('Github_test') // Use your correct GitHub credentials ID
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
                // Clone repo-B where GitHub Pages is hosted
                sh 'git clone https://github.com/jkbarathkumar/auto-trigger-learning.git'

                // Copy the relevant files to repo-B (exclude the repo itself)
                sh 'cp -r Jenkinsfile index.html script.js style.css auto-trigger-learning/'

                // Commit and push the changes to repo-B
                dir('auto-trigger-learning') {
                    sh 'git add .'
                    sh 'git commit -m "Deploy updated code"'
                    sh 'git push https://jkbarathkumar:${GITHUB_TOKEN}@github.com/jkbarathkumar/auto-trigger-learning.git'
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
