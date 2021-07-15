#!/usr/bin/env groovy

node {
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/QDELIE27/test-jenkins'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
   }
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
         //sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         //bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('Connect to REST API') {
       //Yahoo Weather API: Sunset time from Hawaii
       def response = httpRequest 'https://query.yahooapis.com/v1/public/yql?q=select%20astronomy.sunset%20from%20weather.forecast%20where%20woeid%20in%20(select%20woeid%20from%20geo.places(1)%20where%20text%3D%22maui%2C%20hi%22)&format=json&env=store%3A%2F%2Fdatatables.org%2Falltableswithkeys'
       println("Status: "+response.status)
       println("Content: "+response.content)
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      //archive 'target/*.jar'
   }
}
