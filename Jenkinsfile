pipeline { 
    agent  any
    stages {
        stage ('test') {
            steps{
                sh 'echo hello'
            }
        }
        stage('learnig') {
            agent { label 'JAVA-8-MVN' }
            steps {
                git url: 'https://github.com/Giridevops-Git/spring-petclinic.git',
                    branch: 'REAL_2.0.1'
            }
        }
    }
}

