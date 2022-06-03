pipeline{

    agent { label  'JDK11'}
    
    options{
         timeout(time: 1, unit : 'HOURS')
        retry(2)
         
    }

    triggers{
        cron('0 * * * *')
    }

    stages{ 

        stage ('Soucre code') {

            steps {

                 git url:'https://github.com/sunilkumar0454/spring-petclinic.git',

                 branch : 'main'
            }

           
          }

          stage ('Build the code'){

                steps { 

              sh script : 'mvn clean package'

          }

          } 
           stage ('reporting') {

               steps{

               junit testResults:'target/surefire-reports/*.xml'
                    } 

           }

    }

    post {

        success{

            //send the successful email

            echo "success"

            mail bcc: '', body: 'Build success', cc: '', from: 'sunilrb2b@gmail.com', replyTo: '', subject: 'Build succeded', to: 'sunilrb2b@gmail.com'
            
        }

        unsuccessful{

            //send the unsuccessful email

            echo "failure"

        }
    }

}

