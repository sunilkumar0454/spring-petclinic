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

    

}
