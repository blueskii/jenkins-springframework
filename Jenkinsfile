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
        }
        
        stage("Deploy") {
            steps {
                script {
                    RESPONSE = sh(
                		script: "curl -v -u admin:tomcat -T target/*.war 'http://blueskii.synology.me:50003/manage/text/deploy?path=/jenkins-springframework&update=true'", 
                		returnStdout: true
                	).trim()
                	
                	if(RESPONSE.startsWith("OK")) {
                	   echo "OK"       
                	   sh("exit 0")
                	} else {
                	   echo "Fail"
                	   sh("exit 1")   
                	}
                }
            }
        }
    }
}
