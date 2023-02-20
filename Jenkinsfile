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
                    CURL_RESPONSE=$(curl -v -u admin:tomcat -T target/*.war "http://kosa402.iptime.org:50003/manager/text/deploy?path=/jenkins-springframework2&update=true")    
                   
                    /*
                    CURL_RESPONSE="FAIL"
                    if [[ $CURL_RESPONSE == *"FAIL"* ]]; then
                      echo "war deployment failed"
                      exit 1
                    else    
                      echo "war deployed successfully "
                      exit 0
                    fi
                    */
                }
            }
        }
    }
}
