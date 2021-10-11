pipeline{
    agent any
    environment{
        BITBUCKET_CREDS = credentials('javahometech')
        BITBUCKET_PR_BRANCH = "feature/jenkins/mirror-${BUILD_NUMBER}"
        BITBUCKET_PR_DEST_BRANCH = "master"
        PR_TITLE = "PR create by Jenkins ${JOB_NAME}"
        PR_URL = "https://api.bitbucket.org/2.0/repositories/srinivasarao2468/sharedlib/pullrequests"
    }
    stages{
        stage('Git Source Repo'){
            steps{
                dir('sourceRepo'){
                    git url: 'https://github.com/javahometech/sharedlibs', branch: 'main'
                    sh "rm -rf .git"
                }
            }
        }
        stage('Git Dest Repo'){
            steps{
                dir('destRrepo'){
                    withCredentials([gitUsernamePassword(credentialsId: 'bitbucket', gitToolName: 'Default')]) {
                        git url: 'https://srinivasarao2468@bitbucket.org/srinivasarao2468/sharedlib.git', branch: 'master'
                        sh """
                            git checkout -b ${BITBUCKET_PR_BRANCH}
                            cp -R ../sourceRepo/* ./ 
                            git config --global user.name 'Jenkins'
                            git config --global user.email 'jenkins@novartis.com'
                            git add .
                            git commit -m 'create by jenkins for gitlab to bitbucket sync'
                            git push origin ${BITBUCKET_PR_BRANCH}
                        """
                    }
                }
            }
        }
        stage("Create Pull Request"){
            
            steps{
                sh '''
                    curl $PR_URL \
                      -u $BITBUCKET_CREDS_USR:$BITBUCKET_CREDS_PSW \
                      --request POST \
                      --header 'Content-Type: application/json' \
                      --data '{
                        "title": $PR_TITLE,
                        "source": {
                          "branch": {
                            "name": $BITBUCKET_PR_BRANCH
                          }
                        },
                        "destination": {
                            "branch": {
                                "name": $BITBUCKET_PR_DEST_BRANCH
                            }
                        }
                      }'
                '''
            }
        }
    }
    post{
        always{
            cleanWs()
        }
    }
}
