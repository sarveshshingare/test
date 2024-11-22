pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/sarveshshingare/test.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build('sarveshss2513/your-app')
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'my-docker-id') {
                        dockerImage.push()
                    }
                }
            }
        }
       stage('Deploy') {
            steps {
                sshPublisher(
                    publishers: [sshPublisherDesc(
                        configName: 'EC2-server',
                        transfers: [sshTransfer(
                            sourceFiles: '',
                            execCommand: 'docker run -d -p 80:3000 sarveshss2513/your-app'
                        )]
                    )]
                )
            }
        }
}
}
