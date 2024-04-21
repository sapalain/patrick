lnode {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
        app = docker.build("sapalain/jenkinscicd:${env.BUILD_NUMBER}")
    }

    stage('Test image') {
        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        withCredentials([usernamePassword(credentialsId: 'c8c2882a-5887-427a-807d-390292c138c8', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
            docker.withRegistry('https://registry.hub.docker.com', 'c8c2882a-5887-427a-807d-390292c138c8') {
                // Tag the image with the desired tag before pushing
                sh "docker tag sapalain/jenkinscicd:${env.BUILD_NUMBER} sapalain/jenkinscicd:Patrick1"
                // Push the image with the new tag
                app.push("Patrick1")
            }
        }
    }
}
