import static groovy.io.FileType.FILES

pipeline {
   agent { node { label 'S0W1' } }
   
   environment {
      WORKDIR="/u/jenkins/workspace/MortgageApplicationDemo"
	  OUTDIR="/u/jenkins/workspace/MortgageApplicationDemo/output"
      HLQ="IBMUSER.MORTGAGE.JENKINS"
	  APP="MortgageApplicationDemo"
	  DBB_HOME="/usr/lpp/IBM/dbb110"
   }

   stages {
      stage('Check Environment') {
         steps {
            // git the environment variables
            sh 'export PATH=/bin:.:/usr/sbin:/usr/lpp/java/J8.0_64/bin:/usr/lpp/IBM/cobol/igyv6r3/bin:/usr/lpp/IBM/pli/v5r3/bin:/var/rocket/bin'
            sh 'export MANPATH=/usr/man/%L:/var/rocket/man'
            sh 'env'
         }
      }
      
      stage('Git Clone to USS') {
         steps {
            sh 'git config --global http.sslVerify false'
            git branch: 'main', credentialsId: 'GitHubCred', url: 'https://github.com/anuprakashm/MortgageApplicationDemo'
         }
	  }	 
	  
      stage('Build Application') {
         steps {
            sh 'chmod -R 755 $WORKSPACE'
            dir("$WORKSPACE") {
			   sh '$DBB_HOME/bin/groovyz build.groovy --workspace $WORKDIR --application $APP --outDir $OUTDIR --hlq $HLQ --fullBuild'
            }
         }
      }
   }
}
