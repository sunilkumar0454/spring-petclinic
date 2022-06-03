pipeline {

    agent{ label 'JDK11'}

    triggers{

        pollSCM('* * * * *')
        
    }

    stages{
           
            stage('SourceCode'){
                   
                    steps{
                       
                       git branch: 'sprint1_develop', url: 'https://github.com/sunilkumar0454/spring-petclinic.git'

                    }

    }
          stage('Buildsteps'){

              steps{

                 sh 'mvn clean package'

              }
          }

          stage('Archive and Test results')

              { steps{

                 junit '**/surefire-reports/*.xml'
                  archiveArtifacts artifacts: '**/*.jar', followSymlinks: false

              }

                  
              }

              stage('status Build'){

                  steps{

                      echo 'Build success'
                      
                  }
              }

              stage('Email report '){


                steps{

                  mail bcc: '', body: 'Build is success with all the Artifacts and Test Results', cc: 'sunilrb2b@gmail.com', from: '', replyTo: '', subject: 'Build status with   Artifacts and Test Results', to: 'srikanth2107@outlook.com'
              }



              }

              

    }

}