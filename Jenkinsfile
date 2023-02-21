pipeline {
	//Execute this Pipeline or any of its stages, on any available agent
    agent any

	//Declarative Tool
    tools {
        maven "Maven3.8"
    }

    stages {
        stage("Build") {
            steps {
            	//Checkout from SCM(git)
            	git "https://github.com/blueskii/jenkins-springframework/"
            	
            	//Build
				sh "mvn clean package"
            }
        }
        
        stage("Deploy") {
            steps {
                script {
                	//Deploy
                    RESPONSE = sh(
                		script: "curl -v -u admin:tomcat -T target/*.war 'http://blueskii.synology.me:50003/manager/text/deploy?path=/jenkins-springframework&update=true'", 
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
