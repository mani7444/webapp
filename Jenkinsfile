pipeline {
  agent any 
  tools {
    maven 'Maven'
  }
  stages {
    stage ('Initialize') {
      steps {
        sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
      }
    }
    
    stage ('Check-Git-Secrets') {
      steps {
        sh 'rm trufflehog || true'
       // sh 'chmod 666 /var/run/docker.sock'
        sh 'docker run gesellix/trufflehog --json https://github.com/cyclopsbarrack/webapp.git > trufflehog'
        sh 'cat trufflehog'
      }
    }
    
   // stage ('Source Composition Analysis') {
     // steps {
       //  sh 'rm owasp* || true'
         // sh 'wget "https://raw.githubusercontent.com/cehkunal/webapp/master/owasp-dependency-check.sh" '
         // sh 'chmod +x owasp-dependency-check.sh'
         // sh 'bash owasp-dependency-check.sh'
         //sh 'cat /var/lib/jenkins/OWASP-Dependency-Check/reports/dependency-check-report.xml'
        
    //  }
    // }
    
    // stage ('SAST') {
      // steps {
        // withSonarQubeEnv('sonar') {
          // sh 'mvn sonar:sonar'
          // sh 'cat target/sonar/report-task.txt'
       // }
     // }
    // }
    
    stage ('Build') {
      steps {
      sh 'mvn clean package'
       }
    }
    
    // stage ('Deploy-To-Tomcat') {
          //  steps {
          // sshagent(['tomcat']) {
              //  sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@13.232.202.25:/prod/apache-tomcat-8.5.39/webapps/webapp.war'
             // }      
         //  }       
   // }
     
    
    // stage ('DAST') {
      // steps {
       // sshagent(['zap']) {
         // sh 'ssh -o  StrictHostKeyChecking=no ubuntu@13.232.158.44 "docker run -t owasp/zap2docker-stable zap-baseline.py -t http://13.232.202.25:8080/webapp/" || true'
       // }
      // }
   // }
 
    stage ('Upload Reports to Defect Dojo') {
		    steps {
			sh 'pip install requests'
			sh 'wget https://raw.githubusercontent.com/devopssecure/webapp/master/upload-results.py'
			sh 'chmod +x upload-results.py'
			sh 'python upload-results.py --host 18.191.136.107:8080 --api_key 6f753d875fbd8a855781f9245eaaa7b893a2c2a4 --engagement_id 4 --result_file trufflehog --username admin --scanner "SSL Labs Scan"'
    
  }
}
