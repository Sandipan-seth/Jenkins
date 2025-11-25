pipeline {
    agent any

    environment {
        GIT_URL = "https://github.com/Sandipan-seth/Jenkins.git"
        GIT_CREDENTIALS = "git-creds"
    }

    stages {

        stage('Clone Repo') {
            steps {
                git url: "${GIT_URL}", branch: "main", credentialsId: "${GIT_CREDENTIALS}"
            }
        }

        stage('Append to File') {
            steps {
                script {
                    def line = "Entry added at: ${new Date()}\n"

                    // If file exists → read it, append new line
                    // If not → create a new one
                    def oldContent = ""
                    if (fileExists("timestamp.txt")) {
                        oldContent = readFile("timestamp.txt")
                    }

                    writeFile file: "timestamp.txt", text: oldContent + line
                }
            }
        }

        stage('Commit & Push') {
            steps {
                script {
                    sh """
                        git config user.email "sandipanseth2004@gmail.com"
                        git config user.name "Sandipan Seth"

                        git add .
                        git commit -m "commiting via Jenkins" || echo "Nothing to commit"
                        git push origin main
                    """
                }
            }
        }
    }
}
