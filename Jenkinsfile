/*pipeline {
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
                    sh 'git push https://$GITHUB_TOKEN@github.com/jkbarathkumar/jkbarathkumar.github.io'
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
 */


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
                script {
                    // Remove the existing auto-trigger-learning directory if it exists
                    sh 'rm -rf jkbarathkumar.github.io'

                    // Clone repo-B (GitHub Pages)
                    sh 'git clone https://github.com/jkbarathkumar/jkbarathkumar.github.io.git'

                    // Copy all files from the current workspace (including renamed/added files)
                    sh 'cp -r * jkbarathkumar.github.io/'

                    // Go to the target directory (auto-trigger-learning)
                    dir('auto-trigger-learning') {
                        // Configure Git identity for Jenkins
                        sh 'git config user.name "Jenkins CI"'
                        sh 'git config user.email "jenkins@yourdomain.com"'

                        // Check the status and add all modified, renamed, or deleted files
                        sh 'git add .'
                        
                        // Commit the changes with a message
                        sh 'git commit -m "Deploy updated code"'

                        // Push the changes to the destination repository
                        sh 'git push https://$GITHUB_TOKEN@github.com/jkbarathkumar/jkbarathkumar.github.io.git'
                    }
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
