pipeline {
    agent any

    environment {
        MONGODB_URI='mongodb+srv://bonfacemasira:l12bhUCkr8n3lvX7@week-2-ip1.wssgel4.mongodb.net/?retryWrites=true&w=majority&appName=week-2-ip1'
        EMAIL_BODY = """
            <p>EXECUTED: Job <b>\'${env.JOB_NAME}:${env.BUILD_NUMBER})\'</b></p>

            <p>

            View console output at

            "<a href="${env.BUILD_URL}">${env.JOB_NAME}:${env.BUILD_NUMBER}</a>"

            </p>

            <p><i>(Build log is attached.)</i></p>
        """

        EMAIL_SUBJECT_SUCCESS = "Status: 'SUCCESS' -Job \'${env.JOB_NAME}:${env.BUILD_NUMBER}\'"

        EMAIL_SUBJECT_FAILURE = "Status: 'FAILURE' -Job \'${env.JOB_NAME}:${env.BUILD_NUMBER}\'"

        EMAIL_RECEPIENT = 'bonfacemasira@gmail.com'
    }

    tools {
        nodejs 'nodejs'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/bonfacemasira/gallery.git'
            }
            post {
                success {
                    slackSend (channel: '#ip1',color: '#00FF00', message: "SUCCESS: Checkout Stage of Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (https://gallery-b4yh.onrender.com)")
                }
                failure {
                    slackSend (channel: '#ip1',color: '#FF0000', message: "SUCCESS: Checkout Stage of Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (https://gallery-b4yh.onrender.com)")
                }
            }
        }

        stage('Build') {
            steps {
                sh 'npm install'
            }
            post {
                success {
                    slackSend (channel: '#ip1', color: '#00FF00', message: "SUCCESS: Build Stage of Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (https://gallery-b4yh.onrender.com)")
                }
                failure {
                    slackSend (channel: '#ip1', color: '#FF0000', message: "FAILURE: Build Stage of Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (https://gallery-b4yh.onrender.com)")
                }
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'
            }
            post {
                success {
                    slackSend (channel: '#ip1', color: '#00FF00', message: "SUCCESS: Test Stage of Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (https://gallery-b4yh.onrender.com)")
                }
                failure {
                    slackSend (channel: '#ip1', color: '#FF0000', message: "FAILURE: Test Stage of Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (https://gallery-b4yh.onrender.com)")
                    emailext attachLog: true, body: EMAIL_BODY, subject: EMAIL_SUBJECT_FAILURE, to: EMAIL_RECEPIENT
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to Render'
            }
            post {
                success {
                    slackSend (channel: '#ip1', color: '#00FF00', message: "SUCCESS: Deploy Stage of Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (https://gallery-b4yh.onrender.com)")
                }
                failure {
                    slackSend (channel: '#ip1', color: '#FF0000', message: "FAILURE: Deploy Stage of Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (https://gallery-b4yh.onrender.com)")
                }
            }
        }
    }
}