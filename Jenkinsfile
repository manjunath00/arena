pipeline {
    agent any

    // triggers {
    //     pollSCM('* * * * *')
    // }

    tools {nodejs "nodejs"}

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
                    sh "npm i && npm run build"
                }
                }
            }
        }

        stage('Copy the files') {
            steps {
                script {
                    sh 'rsync -avz build/* pradmin@discovery1.pickright.internal:/var/www/arena/'
                }
            }
        }
    }
}