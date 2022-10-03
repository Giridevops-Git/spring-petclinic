pipeline {
    agent any
    parameters {
        string(name: 'MAVEN_GOAL', defaultValue: 'clean install', description: 'maven goal')

    }
    triggers {
	@@ -12,35 +11,49 @@ pipeline {
    stages {
        stage('vcs') {
            steps {
                git branch: "jfd_3.0.1", url: 'https://github.com/Giridevops-Git/spring-petclinic.git'
            }

        }
         stage ('Artifactory configuration') {
            steps {
                rtServer (
                    id: "JF-SPC-MVN",
                    url: "https://girish1.jfrog.io/",
                    credentialsId: "JF-SPC-JAVA"
                )

                rtMavenDeployer (
                    id: "Default-Maven",
                    serverId: "JF-SPC-MVN",
                    releaseRepo: 'default-libs-release-local',
                    snapshotRepo: 'default-libs-snapshot-local'
                )


            }
        }

        stage ('Exec Maven') {
            steps {
                rtMavenRun (
                    tool: 'MAVEN_DEFAULT', // Tool name from Jenkins configuration
                    pom: 'pom.xml',
                    goals: 'clean install',
                    deployerId: "MAVEN_DEPLOYER"
                )
            }
        }

        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "JF-SPC-MVN"
                )
            }
        }


    }

}