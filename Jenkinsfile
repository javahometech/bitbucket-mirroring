pipeline{
    agent any
    environment{
        BITBUCKET_CREDS = credentials('javahometech')
    }
    stages{
        stage('Git Mirror'){
            when {
                expression { "Y" == 'x' }
            }
            steps{
                checkout scm
                withCredentials([usernamePassword(credentialsId: 'javahometech', passwordVariable: 'password', usernameVariable: 'userId')]) {
                    dir('my-app') {
                        sh 'git push https://$BITBUCKET_CREDS_USR:$BITBUCKET_CREDS_PSW@github.com/javahometech/my-app.git'
                    }
                    
                }
            }
        }
        stage("Create Pull Request"){
            steps{
                sh """
                    curl -v https://api.bitbucket.org/2.0/repositories/srinivasarao2468/sync-test/pullrequests \
                      -u a.srinivasarao2468@gmail.com:9959144875 \
                      --request POST \
                      --header 'Content-Type: application/json' \
                      --data '{
                        "title": "Hari Kammana Pull Request From Jenkins",
                        "source": {
                          "branch": {
                            "name": "feature/syncdemo"
                          }
                        }
                      }'
                """
            }
        }
    }
}
