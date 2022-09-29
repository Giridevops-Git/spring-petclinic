pipeline {
    agent  { label 'JAVA-8-MVN' }
    parameters {
        choice(name: 'BRANCH_TO_BUILD', choices: ['REAL_2.0.1', 'REAL_1.0.1','main','master'], description: 'Branch to build')
        string(name: 'MAVEN_GOAL', defaultValue: 'package', description: 'maven goal')

    }
     triggers {
        pollSCM('* * * * *')
     }
    stages {
        stage('vcs') {
            steps {
                git branch: 'REAL_2.0.1', url: 'https://github.com/Giridevops-Git/spring-petclinic.git'
                git branch: "${params.BRANCH_TO_BUILD}", url: 'https://github.com/Giridevops-Git/spring-petclinic.git'
            }

        }
        stage('build') {
            steps {
                sh '/opt/apache-maven-3.8.6/bin/mvn package'
                sh "/opt/apache-maven-3.8.6/bin/mvn ${params.MAVEN_GOAL}"
            }
        }
        stage('archive results') {
            steps {
                junit '**/surefire-reports/*.xml'
            }
        }
    }
}