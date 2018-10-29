pipeline {
    agent any
    stages {
        stage('build && SonarQube analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    withMaven(jdk: 'Java', maven: 'Maven') {
                        sh 'mvn clean compile' 
                        //sonar:sonar -Drat.skip=true'
                    }
                }
            }
        }
        
        //stage("Quality Gate") {
          // steps {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
            //        waitForQualityGate abortPipeline: true
           //}
           //}
        stage('Jacoco') {
            steps {
                jacoco()
            }
        }
        stage('Package') {
            steps {
                       withMaven(jdk: 'Java', maven: 'Maven') {
                        sh 'mvn package -Drat.skip=true'
                    }
                }
            stage('Run kubectl') {
                steps {
                            sh "kubectl get pods"
      }
    }
              }
        }
    }

