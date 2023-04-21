currentBuild.displayName="mahesh#${currentBuild.number}"
pipeline {
    agent any

    stages{
        
         stage('git checkout') {
             when{
            expression{
            params.BranchName=="develop"
            }
        }
             steps {
                git url: 'https://github.com/maheshmcs/hr-api', branch: "${params.BranchName}"
            }
        }
        stage('maven build') {
            when{
            expression{
            params.BranchName=="develop"
            }
        }
            steps {
                sh 'mvn clean package'
            }
        }
        stage('tomcat deploy-dev') {
            steps {
                sshagent(['tomcat-dev']) {
                    sh 'scp -o StrictHostKeyChecking=no target/hr-api.war ec2-user@172.31.46.54:/opt/tomcat9/webapps/'
                    sh 'ssh ec2-user@172.31.46.54 /opt/tomcat9/bin/shutdown.sh'
                    sh 'ssh ec2-user@172.31.46.54 /opt/tomcat9/bin/startup.sh'
                }
            }
        }
    }
         post {
            always {
              cleanWs()
        }
    }
}
