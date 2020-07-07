pipeline {
    agent any

    //tools {
      //  maven "3.6.0" // You need to add a maven with name "3.6.0" in the Global Tools Configuration page
    //}

    stages {
       // stage("Build") {
         //   steps {
               // sh "mvn -version"
               
          //      sh "mvn clean install"
           // }
      //  }
        stage("build & SonarQube analysis") {
            agent any
            steps {
              withSonarQubeEnv('My SonarQube Server') {
                sh 'mvn clean package sonar:sonar'
              }
            }
        }
        stage("Quality Gate") {
            steps {
              timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
              }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}

//git credentialsId: 'git', url: 'ssh://git@192.168.15.5:30022/root/firstproject.git'