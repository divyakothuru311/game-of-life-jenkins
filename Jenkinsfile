pipeline{
    agent { label 'JDK_8' }
    options {
        timeout(time: 10, unit: 'MINUTES') 
    }
    triggers { pollSCM('* * * * *') }
    tools{
        jdk 'JDK_8'
    }
    stages{
        stage('vcs') {
            steps{
                git url: 'https://github.com/divyakothuru311/game-of-life-jenkins.git'
                    branch: 'master'
            }
        }
        stage('build n package') {
            steps{
                sh script : 'mvn package'
            }
        }
        stage('reports') {
            steps{
                archiveArtifacts artifacts: 'target/*.war'
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
    }
}