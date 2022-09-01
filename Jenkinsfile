pipeline {
    agent none
    stages {
        stage ('stage-1') {
            agent { label 'jenkins-agent-1' }
            steps {
                echo "Hello stage-1"
            }
        }
        stage ('stage-2') {
            agent { label 'jenkins-agent-2' }
            steps {
                echo "Hello stage-2"
            }
        }
    }
}
