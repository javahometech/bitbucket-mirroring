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
    }
}
