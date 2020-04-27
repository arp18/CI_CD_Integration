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
		   publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'addressbook_main/target/site', reportFiles: 'surefire-report.html', reportName: 'SureFireHtml', reportTitles: ''])
	  }
	  catch(err){
	     throw err
	  }
	  }
	  stage('Package and generate artifacts'){
	      try{
		      sh "$MVNHOME/bin/mvn clean package -Dskiptests=true"
			  archiveArtifacts allowEmptyArchive: true, artifacts: 'addressbook_main/target/**/*.war', followSymlinks: false
			  
	  }
	      catch(err){
		           throw err
		  }
		  }
		  
		  stage('Deployment Applicaiton using docker'){
		       try{
			        sh "docker version"
					//sh "docker rm $(docker ps -a -q)"
					sh "docker build -t arp181277/deployment:latest -f Dockerfile ."
					sh "docker run -p 8080:8080 -d arp181277/deployment:latest"
					withDockerRegistry(credentialsId: 'dockerhub') {
                      
					  sh "docker push arp181277/deployment:latest"
	               
                   }
			   
			   }
			   catch(err){
			         throw err
			   }

		  }

}
