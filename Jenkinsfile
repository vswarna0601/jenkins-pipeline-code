pipeline {
    agent none
    tools {
        maven "mymaven"
        jdk   "myjava"
    }
    stages {
        stage('compile') {
            agent {
                label 'windows_aws_slave'
            }
            steps {
                git "https://github.com/devops-trainer/DevOpsClassCodes.git"
                bat "mvn compile"
            }
        }
        stage ('codereview') {
            agent {
                label "windows_machine"
            }
            steps {
                git "https://github.com/devops-trainer/DevOpsClassCodes.git"
                bat "mvn pmd:pmd"
            }
        }
        stage ('unittest') {
            agent {
                label 'Linux_Slave'
            }
            steps {
                git "https://github.com/devops-trainer/DevOpsClassCodes.git"
                sh "mvn test" 
            }
        }
        stage ("metriccheck") {
            agent any
            steps {
                git "https://github.com/devops-trainer/DevOpsClassCodes.git"
                sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
            }
        }
        stage ("package") {
            agent {
                label 'windows_machine'
            }
            steps {
                git "https://github.com/devops-trainer/DevOpsClassCodes.git"
                bat 'mvn package'
            }
        }
    }
}
