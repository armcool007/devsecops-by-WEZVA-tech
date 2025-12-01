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
              sh "sed -i 's/image: armcool004.*/image: armcool004\\/democicd_adman_devsecops:$IMAGETAG/g' deployment.yml" 
	    }
    }
  }
 }
}

