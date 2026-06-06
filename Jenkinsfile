pipeline {
    agent any
    stages {

        stage("git_checkout") {
            steps {
                echo "cloning repository"
                git branch: 'main',
                    url: 'https://github.com/Charan-bavaji/onlinebookstore.git'
                echo "repo cloned successfully"
            }
        }

    }
}
