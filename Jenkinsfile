#!groovy
node('slave1') {
   // Mark the code checkout 'stage'....
   stage ('Checkout'){
      checkout([$class: 'GitSCM', 
      branches: [[name: '*/master']], 
      doGenerateSubmoduleConfigurations: false, 
      extensions: [], 
      submoduleCfg: [], 
      userRemoteConfigs: [[url: 'https://github.com/gustavo-dulman/gradle-hello-world.git']]])
   }

   // Mark the code build 'stage'....
   stage ('Build'){
   //branch name from Jenkins environment variables
   echo "My branch is: ${env.BRANCH_NAME}"
   def flavor = flavor(env.BRANCH_NAME)
   echo "Building flavor ${flavor}"

   //build your gradle flavor, passes the current build number as a parameter to gradle
   sh "./gradlew clean assemble${flavor}Debug -PBUILD_NUMBER=${env.BUILD_NUMBER}"
   }
}
