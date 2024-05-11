pipeline {
    agent { label "Jenkins-Agent" }
    environment {
              APP_NAME = "register-app-pipeline"
    }

    stages {
        stage("Cleanup Workspace") {
            steps {
                cleanWs()
            }
        }

        stage("Checkout from SCM") {
               steps {
                   git branch: 'main', credentialsId: 'github', url: 'https://github.com/Abrar-Akbar/gitops-register-app-java.git'
               }
        }

        stage("Update the Deployment Tags") {
            steps {
                sh """
                   cat deployment.yaml
                   sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yaml
                   cat deployment.yaml
                """
            }
        }

        stage("Push the changed deployment file to Git") {
            steps {
                sh """
                   git config --global user.name "Abrar Akbar"
                   git config --global user.email abrarakbar623@gmail.com"
                   git config --global credential.https://github.com/Abrar-Akbar/gitops-register-app-java.git github_pat_22GGKOLFDc0bXEsXOySzY_0T4UeHNbfpysY093TT8ON0MmfXxouc8rlcQqA4vGVfdsGFREW
                   git add deployment.yaml
                   git commit -m "Updated Deployment Manifest"
                   git push https://Abrar-Akbar:github_pat_22GGKOLFDc0bXEsXOySzY_0T4UeHNbfpysY093TT8ON0MmfXxouc8rlcQqA4vGVfdsGFREW@github.com/Abrar-Akbar/gitops-register-app-java main
                """
                // withCredentials([string(credentialsId: 'token1', variable: 'token1', gitToolName: 'Default')]){
                //   sh "git push https://github.com/Abrar-Akbar/gitops-register-app-java.git main"
                // }
            }
        }
      
    }
}
