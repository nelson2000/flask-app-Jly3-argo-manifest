node {

        def app

        stage("clone repository") {
            
            checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/nelson2000/ms-python-flask-sample.git']])
        }


        stage("Update Git"){

            script {

                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github_cred', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME' )]){

                        sh "git config user.email nwajienelson@gmail.com"
                        sh "git config user.name nelson"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+nwajienelson/pythonapp*+nwajienelson/pythonapp:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        SH "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/argo-yaml.git HEAD:main"
                }
               
            }
        }

  

    }
}  