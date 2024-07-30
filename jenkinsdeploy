pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Deploy') {
            steps {
                script {
                    def serverUrl = 'http://35.154.168.2:8080/manager/text'
                    def credentialsId = 'tomcat_crd'

                    withCredentials([usernamePassword(credentialsId: credentialsId, passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
                        sh "curl --user $USERNAME:$PASSWORD --upload-file target/works-with-heroku-1.0.war ${serverUrl}/deploy?path=/works-with-heroku"
                    }
                }
            }
        }
    }
}
