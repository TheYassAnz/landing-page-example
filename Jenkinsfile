pipeline {
    agent any

    stages {
        stage('Pull repository') {
            steps {
                git branch: 'main', url: 'https://github.com/fredericEducentre/landing-page-example.git'
            }
        }

        stage('Deploy') {
            steps {
                sshagent(credentials: ['05a64152-0fbb-4882-bdc2-357bc9d884ac']) {
                    sh '''
                        scp -o StrictHostKeyChecking=no -r ./* \
                        yassine-efrei@ssh-yassine-efrei.alwaysdata.net:~/www/
                    '''
                }
            }
        }
    }
}