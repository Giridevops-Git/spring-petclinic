pipeline {
    agent any
    parameters {
        string(name: 'MAVEN_GOAL', defaultValue: 'clean install', description: 'maven goal')
      }
      stages {
        stage('vcs') {
            steps {
                git branch: "jfd3_0.1", url: 'https://github.com/Giridevops-Git/spring-petclinic.git'
            }
        }
         stage ('Artifactory configuration') {
            steps {
                rtMavenDeployer (
                    id: "MAVEN_DEPLOYER",
                    serverId: "JF-SPC-MVN",
                    releaseRepo: 'default-libs-release-local',
                    snapshotRepo: 'default-libs-snapshot-local'
                )
            }
        }
        stage ('Exec Maven') {
            steps {
                rtMavenRun (
                    tool: 'Default_Maven', // Tool name from Jenkins configuration
                    pom: 'pom.xml',
                    goals: 'clean install',
                    deployerId: "MAVEN_DEPLOYER"
                )
            }
        }
    }
}