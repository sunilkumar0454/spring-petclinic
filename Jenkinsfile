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

            git url:'https://github.com/sunilkumar0454/spring-petclinic.git'
            
            branch : 'main'
          }

          stage ('Build the code') { 

              sh script : 'mnv clean package'

         }
           stage ('reporting') {

               junit testResults:'target/surfire-reports/*.xml'

           }               

    }

    post {

        sucess{

            //send the successful email

            echo 'success'
        }

        unsuccessful{

            //send the unsuccessful email

            echo : 'failure'

        }
    }

}