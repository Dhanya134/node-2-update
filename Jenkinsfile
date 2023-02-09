pipeline {
    
    agent any
    stages {
        stage("Checkout") {
            steps {

               checkout scm
        }
            
            
    }
        
        stage("update git"){
        steps{
            withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'pass', usernameVariable: 'user')]) {
                  script {
                        env.encodedPass=URLEncoder.encode(pass, "UTF-8")
                    }
    

        sh "git config user.email dhanyashree@persistent.com"
        sh "git config user.name Dhanya134"
        sh "cat ./dev/backend.yaml"
        echo "${DOCKERTAG}"
        sh "sed -i 's+image-registry.openshift-image-registry.svc:5000/dhanya-jenkins/node-gitserver.*+image-registry.openshift-image-registry.svc:5000/dhanya-jenkins/node-gitserver:${DOCKERTAG}+g' ./dev/backend.yaml"
        sh "cat ./dev/backend.yaml"
        sh "git add ."
        sh "git commit -m 'done by jenkins job node-app-update-deployment-pipeline-back' "
        sh "git checkout branch"
        sh "git fetch origin"
        sh "git merge origin/branch"
        sh  'git push https://$user:$encodedPass@github.com/$user/node-2-update.git HEAD:branch'
            }
        }
        }
        }
}
