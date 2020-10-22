pipeline{
        agent any  
          stages {
            stage('SCM') {
              steps {
                   git 'https://github.com/amar5607/sonar_3.git'
                   }
                         }
             stage('Quality Gate Statuc Check'){
                  steps{
                      script{
                       withSonarQubeEnv('sonarserver') { 
                       sh "mvn sonar:sonar"
                        }
		       sleep(90)
                       timeout(time: 2, unit: 'MINUTES') {
                       def qg = waitForQualityGate()
                       if (qg.status != 'OK') {
                       error "Pipeline aborted due to quality gate failure: ${qg.status}"
                      }
                    }
		    sh "mvn clean package"
                  }
                }  
              }

             }

        }
