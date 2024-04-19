pipeline {
    agent any 

    tools {
        nodejs '16.20.2'
    }

    stages {
        stage('build') {
            steps {
                sh "npm install"
                sh "npm run build"
            }
        }

        stage('deploy') {
            steps {
                sh "rm -r /var/www/jenkins-test"
                sh "cp -r ${WORKSPACE}/build/ /var/www/jenkins-test/" 
            }
        }
    }

    
}