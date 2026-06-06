pipeline {
    agent any
    stages {

        stage("git_checkout") {
            steps {
                echo "cloning repository"
                git branch: 'main',
                    url: 'https://github.com/YOUR-USERNAME/YOUR-REPO.git'
                echo "repo cloned successfully"
            }
        }

    }
}
