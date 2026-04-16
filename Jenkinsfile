node {
    stage("Checkout GITHUB") {
        checkout scm
    }
    stage("Test using JUNIT testing") {
        sh "mvn test"
    }
    stage("Build using Maven") {
        sh "mvn clean package"
    }
    stage("Create Docker image") {
        sh "docker build -t sanjaikumar1one/movie-rating:latest ."
    }
    stage("Push to Docker Hub") {
        withCredentials([usernamePassword(credentialsId: "docker-hub-login", passwordVariable: "PASS", usernameVariable: "USER")]) {
            sh "echo $PASS | docker login -u $USER --password-stdin"
            sh "docker push sanjaikumar1one/movie-rating:latest"
        }
    }
}