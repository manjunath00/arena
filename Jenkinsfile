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
                    // Define source directory as the workspace
                    def sourceDirectory = "${WORKSPACE}/build/"
                    
                    // Copy files using rsync
                    // Replace 'your_ssh_credential_id' with the ID of your SSH credentials
                    // Replace 'user@hostname' with the appropriate credentials for the destination machine
                    // Replace '<destination_directory>' with the desired destination directory on the remote machine
                    withCredentials([sshUserPrivateKey(credentialsId: 'jenkins-ssh-key	', keyFileVariable: 'SSH_KEY')]) {
                        sh "rsync -avz -e 'ssh -i $SSH_KEY' $sourceDirectory pradmin@discovery1.pickright.internal:/var/www/arena/"
                    }
                }
            }
        }
    }
}