// This Jenkinsfile created on Looping concept.
def chaitu = [
    dockerbuild: "docker build -t chaitu1812/noderun .",
    dockerpush: "docker push chaitu1812/noderun",
    // for docker push u have to login on that server manually
    dockerrmi: "docker rmi chaitu1812/noderun",
]
pipeline
{
    agent {
      // This is job is run in another server, make sure that install git & docker & nginx on that server
      
        label 'NodejsJobs'
    }
    // Global Tool configuration Section
    tools{
        nodejs 'NodeJS17.8.0' 
    }
    options {
     timestamps()
   }
   stages{
       stage('git clone'){
            steps{
                git branch: 'FIRST', url: 'https://github.com/chaithanya1812/test4-Nodejs.git'
            }   
       }
     // This is like looping  
     
       stage("looping"){
           steps {
               script {
                   chaitu.each { entry ->
                    stage(entry.key){
                        sh "$entry.value"
                    }
                   }    
               }
           }
           
       }
     /* Run Containers as you want to run
        And Also update the nginx.confg  file in git-hub present */
       stage('run-cont'){
           steps{
           sh 'docker stop $(docker ps -q)'
           sh 'docker rm  $(docker ps -aq)'   
           sh 'docker run -d --name chaitu1 -p 8081:5555 chaitu1812/noderun'
           sh 'docker run -d --name chaitu2 -p 8082:5555 chaitu1812/noderun'
           sh 'docker run -d --name chaitu3 -p 8083:5555 chaitu1812/noderun'
           sh 'docker run -d --name chaitu4 -p 8084:5555 chaitu1812/noderun'
           sh 'docker run -d --name chaitu5 -p 8085:5555 chaitu1812/noderun'
           }
       }
     // give chmod 777 -R for nginx total directory otherwise it won't work
       stage('ssh-Agent'){
           steps{
               sshagent(['lop']) {
                   sh "scp -o StrictHostKeyChecking=no nginx.conf ec2-user@3.110.193.52:/etc/nginx/nginx.conf"
                   sh "ssh -o StrictHostKeyChecking=no ec2-user@3.110.193.52 sudo systemctl restart nginx"
                  }
           }
       }
   } 
// For more Details refer the Image in README.md File
}   

