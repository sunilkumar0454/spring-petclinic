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

              stage('status Buils'){

                  steps{

                      echo 'Build success'
                      
                  }
              }

                  
              }

    }


}