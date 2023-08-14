pipeline {
    agent { label 'JDK-17' }


     triggers {
        pollSCM ('* * * * *')
     }

     tools {
        jdk 'JDK-8'
     }

     stages {
         stage ('vcs') {
             steps {
                git branch : 'develop',
                    url : 'https://github.com/Bhavana-2022/game-of-life.git'

                
             }

         }
         stage ('build and package') {
            steps {
                rtMavenDeployer(
                    id: 'newgoal',
                    serverId: 'goalinstance',
                    releaseRepo: 'gol-libs-release',
                    snapshotRepo: 'gol-libs-snapshot'

                )
                rtMavenRun (
                    tool: 'maven',
                    pom: 'pom.xml',
                    goals: 'clean install',
                    deployerId: 'newgoal'
                    
                )
                rtPublishBuildInfo(
                    serverId: 'goalinstance'
                )
            }
         }

         stage ('artifacts') {
            steps {
                archiveArtifacts artifacts: '**/*.war'

            }
         }

     }

}