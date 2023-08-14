pipeline {
    agent { label 'JDK-17' }


     triggers {
        pollSCM (* * * * *)
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
                sh script : 'mvn package'
            }
         }

         stage ('artifacts') {
            steps {
                archiveArtifacts artifacts: '**/*.war'

            }
         }

     }

}