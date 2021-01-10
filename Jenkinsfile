pipeline {
    agent any

    stages {
        stage('1-Build') {
            steps {
                echo "Start of Stage Build"
				echo "Building......."
				git credentialsId: 'github-key', url: 'git@github.com:nick1846/docker.git'
				echo "End of Stage Build"
            }
        }
        stage('2-Test') {
            steps {
                echo "Start of Stage Test"
				echo "Testing......."
				echo "End of Stage Build"
            }
        }
        stage('3-Deploy') {
            steps {
                echo "Start of Stage Deploy"
				echo "Deploying......."
				sshPublisher(publishers: [sshPublisherDesc(configName: 'dev-server', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''cd /home/ec2-user/docker-compose ls -la docker-compose up -d''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//home//ec2-user', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '**/*.yml')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
				echo "End of Stage Build"
            }
        }
        stage ('Deploy To Prod') {
        input {
            message "Do you want to proceed for production deployment?"
            }
            steps {
                sh 'echo "Deploy into Prod"'
            }
        }
        stage ('Congratulations!') {
            post {
                // only triggered when blue or green sign
               success {
                    slackSend ...
               }
            }
        }
  }
	
}

