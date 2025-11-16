node {
    stage('Clone infrastructure repo') {
        checkout scm
    }

    stage('Update manifest') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    sh "git config user.email 'jenkins@example.com'"
                    sh "git config user.name 'Jenkins Local'"
                    sh "sed -i 's+yaricks/ci-cd-test:.*+yaricks/ci-cd-test:${params.DOCKERTAG}+g' deployment.yaml"
                    sh "git add deployment.yaml"
                    sh "git commit -m 'Update image tag to ${params.DOCKERTAG}'"
                    sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/ci-cd-test-manifest.git HEAD:main"
                }
            }
        }
    }
}
