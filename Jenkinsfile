pipeline {
    agent { label 'build' }
    parameters {
        password(name: 'PASSWD', defaultValue: '', description: 'GitHub Personal Access Token (PAT)')
        string(name: 'IMAGETAG', defaultValue: '1', description: 'Image Tag to Deploy')
        choice(name: 'environment', choices: ['functional', 'integration', 'regression', 'uat', 'release'], description: 'Select environment')
    }
    stages {
        stage('Deploy') {
            steps {
                // Clone with credentials (so push works)
                sh "git clone --branch master https://armcool007:${params.PASSWD}@github.com/armcool007/devsecops-by-WEZVA-tech.git ."

                // Update image tag
                dir("../kubernetes") {
                    sh "sed -i \"s|image: ar4/.*|image: armcool004/democicd_adman_devsecops:${params.IMAGETAG}|g\" deployment.yml"
                }

                // Configure Git identity
                sh 'git config user.email "bipinkk04@gmail.com"'
                sh 'git config user.name "armcool007"'

                // Commit & Push
                sh 'git add kubernetes/deployment.yml'
                sh "git commit -m \"New deployment for Build ${params.IMAGETAG}\""
                sh 'git push origin master'
            }
        }
    }
}
