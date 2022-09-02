pipeline {
    agent none

    environment {
        MY_ENV_VAR = 'hello world'
    }

    stages {

        stage ('parallel') {
            parallel {
                stage ('thread-1') {
                    agent { label 'jenkins-agent-1' }
                    steps {
                        echo "parallel, thread-1"
                    }
                }
                stage ('thread-2') {
                    agent { label 'jenkins-agent-2' }
                    steps {
                        echo "parallel, thread-2"
                    }
                }
                stage ('thread-3') {
                    agent { label 'jenkins-agent-3' }
                    steps {
                        echo "parallel, thread-3"
                    }
                }
            }
        }

        stage ('when') {
            agent { label 'jenkins-agent-3' }
            when {
                environment(name: "MY_ENV_VAR", value: "hello world")
            }

            steps {
                echo "${MY_ENV_VAR}"
                sh 'printenv'
            }
        }

        stage ('execute_scripts') {
            agent { label 'jenkins-agent-1' }
            steps {
                timeout(time: 3, unit: 'SECONDS') {
                    sh './script.sh'
                }
            }
        }

        stage ('do_something_in_addition') {
            agent { label 'jenkins-agent-2' }
            steps {
                sh 'sudo apt update'
            }
        }
    }

    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}
