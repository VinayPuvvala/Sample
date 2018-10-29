pipeline {
    agent any
    stages {
        stage('build && SonarQube analysis') {
            steps {
                //withSonarQubeEnv('SonarQube') {
                   withMaven(jdk: 'Java', maven: 'Maven') {
                      sh 'mvn clean compile -Drat.skip=true' 
                        //sonar:sonar -Drat.skip=true'
                    }
                }
            }
       // }
        
        //stage("Quality Gate") {
          // steps {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
            //        waitForQualityGate abortPipeline: true
           //}
           //}
       // stage('Jacoco') {
         //   steps {
           //     jacoco()
//            }
  //      }
    //    stage('Package') {
      //      steps {
        //               withMaven(jdk: 'Java', maven: 'Maven') {
          //              sh 'mvn package -Drat.skip=true'
            //        }
              //  }
        //}
            stage('Build Docker Image') {
            
            steps {
                script {
                    app = docker.build(vpuvvala/maven)
                    app.inside {
                        sh 'echo $(curl 18.206.96.209:9000)'
                    }
                }
            }
        }
        stage('Push Docker Image') {
            
            steps {
                script {
                    docker.withRegistry('https://hub.docker.com/r/vpuvvala/demo/', 'docker_hub_login') {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
        //stage('DeployToProduction') {
            
            //steps {
                //input 'Deploy to Production?'
               // milestone(1)
                //kubernetesDeploy(
                    //kubeconfigId: 'kubeconfig',
                   // configs: 'sample.yml',
                   // enableConfigSubstitution: true
               // )
           // }
       // }
    }
}

