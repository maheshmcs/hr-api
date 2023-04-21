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
    }
         post {
            always {
              cleanWs()
        }
    }
}
