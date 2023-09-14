//checkout, build, code quality, code coverage, docker build & Push


pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'test', url: 'https://github.com/zielotechgroup/maven-webapp.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package checkstyle:checkstyle'
            }
        }
        stage('Code Quality Check or Static Analysis') {
            steps {
                recordIssues(tools: [checkStyle()])
            }
        }
        stage('Code Coverage') {
            steps {
                jacoco maximumBranchCoverage: '80', maximumClassCoverage: '80', maximumComplexityCoverage: '80', maximumInstructionCoverage: '80', maximumLineCoverage: '80', maximumMethodCoverage: '80', minimumBranchCoverage: '80', minimumClassCoverage: '80', minimumComplexityCoverage: '80', minimumInstructionCoverage: '80', minimumLineCoverage: '80', minimumMethodCoverage: '80'
            }
        }
        stage('Docker Build') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'new', passwordVariable: 'password', usernameVariable: 'username')]) {
                sh 'docker login -u $username -p $password '
                sh 'docker build -t tbhalgat/pipeline .'
                sh 'docker push tbhalgat/pipeline'
                }
             }
        }
    }
}
