pipeline {
    agent any

    tools {
        maven "Maven3.8"
    }

    stages {
        stage('Build') {
            steps {
                git 'https://github.com/blueskii/jenkins-springframework/'
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                success {
                	CURL_RESPONSE = sh (script: 'curl -v -u admin:tomcat -T target/*.war http://kosa402.iptime.org:50003/manager/text/deploy?path=/jenkins-springframework2&update=true', returnStdout: true).trim()
                	
                	echo "${CURL_RESPONSE}"
                }
            }
        }
    }
}
