node {
   def appName
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/wr37ch/hello-world-war.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'M3'
   }
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('Results') {
      // junit '**/target/*/*.xml'
      archive 'target/*.war'
   }
    stage('Sanity check') {
            
                input "Deploy?"
            
        }

   
   stage('Deploy'){
    sh "curl -T target/*.war 'http://admin:admin@ec2-34-244-126-23.eu-west-1.compute.amazonaws.com:8080/manager/text/deploy?path=/jenkins&update=true'"   
   }
   }
