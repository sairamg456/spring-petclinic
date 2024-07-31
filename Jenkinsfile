pipeline {
    agent {
        label 'JDK-17'
    }
    options {
        timeout(time: 30, unit: 'MINUTES')
    }
    triggers {
        pollSCM('* * * * *')
    }
    tools {
        jdk 'JDK_17'
    }
    stages {
        stage ('VSC') {
            steps {
                git url: 'https://github.com/sairamg456/spring-petclinic.git',
                    branch: 'develop' 
            }
        }
    
        stage ('build and package') {
            steps {
                sh script: 'mvn package'
            }
        }
        stage ('reporting') {
            steps {
                archiveArtifacts artifacts: '**/target/spring-petclinic-*.jar'
                junit testResults: '**/target/surefire-reports/TEST-*.xml'
            }

        }
    }
}