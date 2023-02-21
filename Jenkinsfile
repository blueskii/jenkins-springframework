pipeline {
    agent any

    tools {
        maven "Maven3.8"
    }

    stages {
        stage("Build") {
            steps {
                git "https://github.com/blueskii/jenkins-springframework/"
                sh "mvn clean package"
            }

            post {
                success {
                	script {
	                	CURL_RESPONSE = sh (
	                		script: "curl -v -u admin:tomcat -T target/*.war 'http://blueskii.synology.me:50003/manager/text/deploy?path=/jenkins-springframework&update=true'", 
	                		returnStdout: true
	                	).trim()
	                	
	                	echo "-----------------3"
	                	echo "${CURL_RESPONSE}"
	                	echo "-----------------3"
	                }
                }
            }
        }
    }
}
