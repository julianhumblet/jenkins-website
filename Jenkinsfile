pipeline {
    agent any
    triggers {
        pollSCM('H/5 * * * *')
    }
    stages {
        stage('Delete existing files') {
            steps {
                script {
                    def serverHost = '192.168.138.24'
                    def serverUser = 'julian'

                    // Delete existing HTML and CSS files
                    sshagent(['ssh_creds']) {
                        sh "ssh -v ${serverUser}@${serverHost} sudo rm -rf /var/www/html/*"
                    }
                }
            }
        }

        stage('Deploy files to webserver') {
            steps {
                script {
                    // Define your Ubuntu server details
                    def serverHost = '192.168.138.24'
                    def serverUser = 'julian'
                    def remotePath = '/var/www/html/'

                    // Copy the HTML and CSS files to the server
                    sshagent(['ssh_creds']) {
                        sh "scp -r ./* ${serverUser}@${serverHost}:${remotePath}"
                    }
                }
            }
        }
    }
}
