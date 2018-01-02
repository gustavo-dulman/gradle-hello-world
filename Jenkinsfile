#!groovy
node('slave1') {
 gradle4 = tool 'gradle4'
 stage ('chekcout'){
    checkout scm
 }
 stage ('build')
 {
     sh "${gradle4}/bin/gradle jar"
 }
 stage ('unit-test')
 {
     sh "${gradle4}/bin/gradle test"
     junit "build/test-results/junit-platform/*.xml"
 }
 stage ('int-test')
 {
     testData = readFile "test-data/names"
     println testData
     tests = testData.split('\n')
     branches = [:]
     for (test in tests){
         println "line is $test"
         entry = test.split(':')
         branches["${entry[0]}"] = {
            sh script : "test-data/int-test.sh build/libs/oto-gradle-1.0.jar ${entry[0]} '${entry[1]}'"
         }
      }
      parallel branches
   }
 }                  
