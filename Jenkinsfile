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
                mail subject: "Build Started for Jenkins JOB $env.JOB_NAME", 
                  body: "Build Started for Jenkins JOB $env.JOB_NAME", 
                  to: 'giriaws2022@gmail.com'
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
    }
    post {
        always {
            echo 'Job completed'
            mail subject: "Build Completed for Jenkins JOB $env.JOB_NAME", 
                  body: "Build Completed for Jenkins JOB $env.JOB_NAME \n Click Here: $env.JOB_URL",, 
                  to: 'giriaws2022@gmail.com'
        }
        failure {
            mail subject: "Build Failed for Jenkins JOB $env.JOB_NAME with Build ID, 
                  body: "Build Failed for Jenkins JOB $env.JOB_NAME", 
                  to: 'giriaws2022@gmail.com' 
        }
        success {
            junit '**/surefire-reports/*.xml'
        }
    }
}