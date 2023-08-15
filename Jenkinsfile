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
          stage('SonarQube analysis') {
            steps {

                // performing sonarqube analysis with "withSonarQubeENV(<Name of Server configured in Jenkins>)"
                withSonarQubeEnv('SONAR_CLOUD') {
                // requires SonarQube Scanner for Maven 3.2+
                    sh 'mvn clean package org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=bhavana123_gameoflife'
                }
            }
        }

         stage ('artifacts') {
            steps {
                archiveArtifacts artifacts: '**/*.war'

            }
         }

     }

}