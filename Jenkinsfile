pipeline {
    agent any
    stages {
        stage('build && SonarQube analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    // Optionally use a Maven environment you've configured already     
                    withMaven(jdk: 'Java', maven: 'Maven') {
                        // some block
                        sh 'mvn clean package sonar:sonar -Drat.skip=true'
                    }
                }
            }
        }
        stage('Jacoco') {
            steps {
                jacoco()
            }
        }
        stage("Quality Gate") {
            steps {
               timeout(time: 120, unit: 'SECONDS') {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
                    // Requires SonarQube Scanner for Jenkins 2.7+
                    waitForQualityGate abortPipeline: true
                }
           }
        }
        }
    }

