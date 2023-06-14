node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'GITHUBPERSONAL', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        println "Username: ${GIT_USERNAME}"
                        println "Password: ${GIT_PASSWORD}"
                        sh "git status"
                        sh "git config user.email leelavathidh22@gmail.com"
                        sh "git config user.name leelavathidh192"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+leelavathidh/test_repo_docker_image.*+leelavathidh/test_repo_docker_image:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git HEAD:main"
      }
    }
  }
}
}
