pipeline{
    agent any
    environment{
        BITBUCKET_CREDS = credentials('javahometech')
    }
    stages{
        stage('Git Mirror'){
            steps{
                checkout scm
                withCredentials([usernamePassword(credentialsId: 'javahometech', passwordVariable: 'password', usernameVariable: 'userId')]) {
                    dir('bitbucket-mirroring') {
                        sh 'git push https://$BITBUCKET_CREDS_USR:$BITBUCKET_CREDS_PSW@github.com/javahometech/bitbucket-mirroring.git master'
                    }
                    
                }
            }
        }
    }
}
