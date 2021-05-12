if(env.BRANCH_NAME == "master") {
    tag = "latest"
}
else { 
    tag = env.BRANCH_NAME
}

node("docker"){
    stage("Pull Repo"){
        checkout scm
    }

    withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', passwordVariable: 'REGISTRY_PASSWORD', usernameVariable: 'REGISTRY_USERNAME')]) {
        stage("Docker Build"){
            sh "docker build -t ${REGISTRY_USERNAME}/melodi:${tag}  ."
        }
        
        stage("Docker Login"){
            sh "docker login -u ${REGISTRY_USERNAME} -p '${REGISTRY_PASSWORD}'"
        }

        stage("Docker Push"){
            sh "docker push ${REGISTRY_USERNAME}/melodi:${tag}"
        }
    }
}
