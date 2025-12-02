pipeline {
 agent { label 'demo' }
 parameters {
     password(name: 'PASSWD', defaultValue: '', description: 'Please Enter your Gitlab password')
     string(name: 'IMAGETAG', defaultValue: '1', description: 'Please Enter the Image Tag to Deploy?')
     choice(name:'environment', choices: ['functional', 'integration', 'regression', 'uat', 'release' ] ,description: 'select where need to deploy')
 }
 stages {
  stage('Deploy')
  {
    steps { 
        git branch: 'master', credentialsId: 'GitlabCred', url: 'https://github.com/armcool007/devsecops-by-WEZVA-tech.git'
      dir ("./${params.environment}") {
              //sh "sed -i 's/image: armcool004.*/image: armcool004\\/democicd_adman_devsecops:$IMAGETAG/g' deployment.yml"
		  	  sh "sed -i \"s|image: ar4/.*|image: ar4/democicd_adman_devsecops:${params.IMAGETAG}|g\" deployment.yml"
	    }
        sh 'git commit -a -m "New deployment for Build $IMAGETAG"'
	    sh "git push https://armcool007:$PASSWD@github.com/armcool007/devsecops-by-WEZVA-tech.git"

    }
  }
 }
}





