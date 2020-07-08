#!groovy
pipeline {
    agent any

    //tools {
      //  maven "3.6.0" // You need to add a maven with name "3.6.0" in the Global Tools Configuration page
    //}

    stages {
       /**  stage("Build") {
            steps {
                sh "mvn -version"
               
               sh "mvn clean install"
            }
        }
        stage("build & SonarQube analysis") {
            agent any
            steps {
              withSonarQubeEnv('SonarQubeSeverver') {
                sh 'mvn clean package sonar:sonar'
              }
            }
        }**/
        stage("Quality Gate") {
          steps{
                      script{
                      withSonarQubeEnv('SonarQubeSeverver') { 
                      sh "mvn sonar:sonar"
                       }
                      timeout(time: 1, unit: 'HOURS') {
                      def qg = waitForQualityGate()
                      if (qg.status != 'OK') {
                           error "Pipeline aborted due to quality gate failure: ${qg.status}"
                      }
                    }
		    sh "mvn clean install"
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