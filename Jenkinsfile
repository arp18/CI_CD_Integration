def MVNHOME
node('ec2-node'){
    stage('git Checkout'){
        git credentialsId: 'Github_token', url: 'https://github.com/arp18/CI_CD_Integration.git'
    }
	stage('Maven Test'){
	  try{
	       MVNHOME=tool 'Maven-3.0'
		   sh "$MVNHOME/bin/mvn --version"
		   sh "$MVNHOME/bin/mvn clean test surefire-report:report"
	  }
	  catch(err){
	             sh "echo error defining maven test surefire-report:report"
	  }
	  }
	  stage('Testcases and Report'){
	  try{
	       echo "Executing test cases"
		   junit allowEmptyResults: true, testResults: 'addressbook_main/target/surefire-reports/*.xml'
		   publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'pipeline/addressbook_main/target/site/*.html', reportFiles: 'surefire-report.html', reportName: 'surefire-report.html', reportTitles: ''])
	  }
	  catch(err){
	     throw err
	  }
	  }

}
