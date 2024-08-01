pipeline {
    agent {
        label 'JDK'
    }
    options {
        timeout(time: 30, unit: 'MINUTES')
    }
    triggers {
        pollSCM('* * * * *')
    }
    parameters {
        choice(name: 'GOAL', choices: ['package', 'clean package', 'install', 'clean install'], description: 'this is mvn package')
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
                sh script: "mvn ${params.GOAL}"
            }
        }
        stage ('reporting') {
            steps {
                archiveArtifacts artifacts: '**/target/spring-petclinic-*.jar'
                junit testResults: '**/target/surefire-reports/TEST-*.xml'
            }

        }
    }
    post {
        success {
            mail subject: "${JOB_NAME} is effective",
                 body: "your project is effective and Build Url ${BUILD_URL}",
                 to: 'all@jenkins.com'
        }
        failure {
            mail subject: "${JOB_NAME} is deffective",
                 body: "your project is effective and Build Url ${BUILD_URL}",
                 to: 'all@jenkins.com'
        }
    }
}
