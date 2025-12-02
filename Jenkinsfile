pipeline {
 agent { label 'build' }
 parameters {
     string(name: 'IMAGETAG', defaultValue: '1', description: 'Please Enter the Image Tag to Deploy?')
     choice(name:'environment', choices: ['functional', 'integration', 'regression', 'uat', 'release' ] ,description: 'select where need to deploy')
 }
 stages {
  stage('Deploy') {
    steps { 
        git branch: 'master', credentialsId: 'github', url: 'https://github.com/armcool007/devsecops-by-WEZVA-tech.git'

        dir ("./${params.environment}") {
              sh "cp ../kubernetes/* ."
              sh "sed -i \"s|image: armcool004/.*|image: armcool004/democicd_adman_devsecops:${params.IMAGETAG}|g\" deployment.yml"
        }

        // Use credentials securely for push
        withCredentials([usernamePassword(credentialsId: 'github', usernameVariable: 'USER', passwordVariable: 'TOKEN')]) {
            sh """
                git add .
                git commit -m "New deployment for Build ${params.IMAGETAG}" || echo "Nothing to commit"
                git push https://${USER}:${TOKEN}@github.com/armcool007/devsecops-by-WEZVA-tech.git
            """
        }
    }
  }
 }
}
