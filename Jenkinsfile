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
        //   sh 'wget "https://raw.githubusercontent.com/cehkunal/webapp/master/owasp-dependency-check.sh" '
         // sh 'chmod +x owasp-dependency-check.sh'
         // sh 'bash owasp-dependency-check.sh'
        // sh 'cat /var/lib/jenkins/OWASP-Dependency-Check/reports/dependency-check-report.xml'
        
     // }
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
          // sh 'ssh -o  StrictHostKeyChecking=no ubuntu@18.116.25.211 "docker run -t owasp/zap2docker-stable zap-baseline.py -t http://testphp.vulnweb.com/" || true'
       // }
      // }
   // }
 
   stage ('Upload Reports to Defect Dojo') {
		 steps {
			sh 'pip install requests'
			sh 'wget https://raw.githubusercontent.com/cyclopsbarrack/webapp/master/upload-results.py'
			sh 'chmod +x upload-results.py'
		//	sh 'python upload-results.py --host 18.222.203.246:8080 --api_key 00ab3cf66d960a3513fc9c819894826e7563361c --engagement_id 1 --result _file nmap --username admin --scanner "Nmap Scan"'   
			sh 'python upload-results.py --host 18.222.203.246:8080 --api_key 0bbb936d125393eb4ab4a655f66bf1b3f5f4734d --engagement_id 2 --result_file trufflehog --username admin --scanner "Trufflehog"'
                  //    sh 'python upload-results.py --host 13.59.142.183:8080 --api_key d915aad678f94b1ca7fde4eb4016d8cc1d45a788 --engagement_id 5 --result_file /var/lib/jenkins/OWASP-Dependency-Check/reports/dependency-check-report.xml --username admin --scanner "Dependency Check Scan"'
 }
 }
  }
}
