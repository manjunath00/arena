pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage('Git Pull') {
            steps {
                dir('/home/pradmin/repo/web/arena') {
                    deleteDir()

                    // Checkout code from Git repository
                    git branch: 'main', url: 'https://github.com/manjunath00/arena.git'
                }
            }
        }

        stage('NPM Install') {
            steps {
                script {

                dir('/home/pradmin/repo/web/arena/') {
                    sh "rsync -av --delete ${WORKSPACE}/build/* /var/www/jenkins-test/" 
                }
                }
            }
        }
    }
}