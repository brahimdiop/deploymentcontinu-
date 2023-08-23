node {
    def app
  
    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'AFRILINS_TOKEN', passwordVariable: 'BITBUCKET_PASSWORD', usernameVariable: 'BITBUCKET_USERNAME')]) {
                         //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email ibrahima.diop@afrilins.net"
                        sh "git config user.name brahimdiop"
                        //sh "git switch master"
                        sh "cat ./administrationmanifestfiles/deployment-front.yaml" //affricher le contenu
                        sh "sed -i 's+brims15/frontadmine.*+brims15/frontadmine:${DOCKERTAG}+g' ./administrationmanifestfiles/deployment-front.yaml"
                        sh "cat ./administrationmanifestfiles/deployment-front.yaml"            

                        sh "git add ." 
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"                 

                        sh "git push https://brahimdiop@bitbucket.org/${BITBUCKET_USERNAME}/kubernetes.git HEAD:deployk8s"
                        sh " git commit -m 'docker tag =================== ${DOCKERTAG}' "
                        
                        
      }
    }
  }
}
}
