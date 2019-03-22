pipeline {
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B clean verify checkstyle:checkstyle pmd:pmd findbugs:findbugs jacoco:prepare-agent test jacoco:report -Djenkins.test.timeout=240' 
            }
        }
    }
    post {
        always {

            recordIssues enabledForFailure: true, tools: [mavenConsole(), java(), javaDoc()]
            recordIssues enabledForFailure: true, tool: checkStyle()
        }
    }
}

