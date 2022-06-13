pipeline{

    agent { label  'JDK11'}
    
    options{
         timeout(time: 1, unit : 'HOURS')
        retry(2)
         
    }

    triggers{
        cron('0 * * * *')
    }

    parameters {
        choice(name: 'GOAL', choices: ['compile', 'package', 'clean package'])
    }

    stages{ 

        stage ('Soucre code') {

            steps {

                 git url:'https://github.com/sunilkumar0454/spring-petclinic.git',

                 branch : 'main'
            }

           
          }

          stage ('Build the and sonarqube-analysis')  {
                         
                     
                    steps {

                            withSonarQubeEnv('SONAR_LATEST') {
                               sh script: "mvn ${params.GOAL} sonar:sonar"

                                       }
                         } 
         
          }
         
        
           stage ('reporting') {

               steps{

               junit testResults:'target/surefire-reports/*.xml'
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

    // post {

      //  success{

            //send the successful email

      //      echo "success"

      //      mail bcc: '', body: "BUILD URL: ${BUILD_URL} TEST RESULTS ${RUN_TESTS_DISPLAY_URL} ", cc: '', from: 'sunilrb2b@gmail.com.com', replyTo: '', 
      //          subject: "${JOB_BASE_NAME}: Build ${BUILD_ID} Succeded", to: 'sunilrb2b@gmail.com'

      //  }

      //  unsuccessful{

            //send the unsuccessful email

      //      echo "failure"

     //       mail bcc: '', body: "BUILD URL: ${BUILD_URL} TEST RESULTS ${RUN_TESTS_DISPLAY_URL} ", cc: '', from: 'sunilrb2b@gmail.com', replyTo: '', 
     //           subject: "${JOB_BASE_NAME}: Build ${BUILD_ID} Failed", to: 'sunilrb2b@gmail.com'

     //   }
  //  }

}

