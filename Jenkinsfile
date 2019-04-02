node {
  
  stage('Configure') {
    sh 'echo "Already set Maven path at Jenkins Server!"'
   }
  
  stage('Cleanup Workspace')
  {
    sh 'echo "Cleanup Workspace before build starts"'
    deleteDir()
  }
  
  stage('Checkout Source Code') {
   //Checkout Based on Configured Credentials
   sh 'date'
   sh 'pwd' 
   checkout scm
   sh 'git log -n 1'
  }

  stage('Package the war') {
   sh 'sudo docker run --rm -v $(pwd) harshblog150/maven:3.6.0-jdk8 mvn package -f $(pwd)'
  }
 
  stage('Test') {
    junit allowEmptyResults: true, testResults: '**/target/**/TEST*.xml'
  }
  
  stage ('Deploy Application on tomcat Container') {
	sh 'sudo docker run -i -p 8888:8080 -v $(pwd)/target/spring-mvc-showcase.war:/usr/local/tomcat/webapps/spring-mvc-showcase.war harshblog150/tomcat8:jdk8'
  }
}
