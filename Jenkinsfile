pipeline {
    agent any

    tools {
        maven "Maven3.8"
    }

    stages {
        stage("Build") {
            steps {
                git "https://github.com/blueskii/jenkins-springframework/"
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                success {
                	script {
	                	CURL_RESPONSE = sh (
	                		script: "curl -v -u admin:tomcat -T target/jenkins-springframework-1.0.0.war 'http://blueskii.synology.me:50003/manager/text/deploy?path=/jenkins-springframework&update=true'", 
	                		returnStdout: true
	                	).trim()
	                	
	                	echo "-----------------"
	                	echo "${CURL_RESPONSE}"
	                	echo "-----------------"
	                }
                }
            }
        }
    }
}
