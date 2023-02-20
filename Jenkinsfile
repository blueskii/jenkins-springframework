pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "Maven3.8"
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/blueskii/jenkins-springframework/'

                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    echo "success"
                    
                    //junit '**/target/surefire-reports/TEST-*.xml'
                    //archiveArtifacts 'target/*.jar'
                    //CURL_RESPONSE=$(curl -v -u "admin:tomcat" -T target/*.jar "http://kosa402.iptime.org:50003/manager/text/deploy?path=/jenkins-springframework2&update=true")    
                   
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
