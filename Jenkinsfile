pipeline{
    agent any
    environment{
        BITBUCKET_CREDS = credentials('javahometech')
        BITBUCKET_USER = "a.srinivasarao2468@gmail.com"
        BITBUCKET_PWD = "9959144875"
    }
    stages{
        stage('Git Mirror'){
            when {
                expression { "Y" == 'x' }
            }
            steps{
                dir('source-repo'){
                    git url: 'https://github.com/javahometech/sharedlibs'
                }
            }
        }
        stage("Create Pull Request"){
            steps{
                sh """
                    curl -v https://api.bitbucket.org/2.0/repositories/srinivasarao2468/sync-test/pullrequests \
                      -u $BITBUCKET_USER:$BITBUCKET_PWD \
                      --request POST \
                      --header 'Content-Type: application/json' \
                      --data '{
                        "title": "Hari Kammana Pull Request From Jenkins...Again",
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
