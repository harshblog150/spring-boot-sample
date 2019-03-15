node{

  stage('Configure') {
   //env.PATH = "${tool 'maven-3.3.9'}/bin:${env.PATH}"
  sh 'echo "Already set Maven path at Jenkins Server!"'
  }
  stage('Cleanup Workspace')
  {
    sh 'echo "Cleanup Workspace before build starts"'
    deleteDir()
  }
  stage('Checkout Source Code') {
    //git 'https://github.com/bertjan/spring-boot-sample'
   //Checkout Based on Configured Credentials
   sh 'date'
   sh 'pwd' 
   checkout scm
   sh 'git log -n 1'
  }
  stage('Build') {
    sh 'mvn -B -V -U -e clean package'
  }
    
  stage('Test') {
    junit allowEmptyResults: true, testResults: '**/target/**/TEST*.xml'
  }

stage('Deploy') {
    //sh 'scp target/*.jar jenkins@13.127.51.181:/tmp'
      sh 'scp target/*.war jenkins@13.233.168.15:/opt/tomcat/webapps'
      sh 'ssh jenkins@13.233.168.15 java -jar /opt/tomcat/webapps/*.war --server.port=8081'
}
}
