def MVNHOME
node('ec2-node'){
    stage('git Checkout'){
        git credentialsId: 'Github_token', url: 'https://github.com/arp18/CI_CD_Integration.git'
    }
	stage('Maven Test'){
	  try{
	       MVNHOME=tool 'Maven-3.0'
		   sh "$MVNHOME/bin/mvn --version"
		   sh "$MVNHOME/bin/mvn clean test"
	  }
	  catch(err){
	             sh "echo error defining maven test"
	  }
	  }

}
