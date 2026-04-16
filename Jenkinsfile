node {
    stage("Checkout GITHUB") {
        checkout scm
    }
    stage("Test using JUNIT testing") {
        bat "mvn test"
    }
    stage("Build using Maven") {
        bat "mvn clean package"
    }
    stage("Create Docker image") {
        bat "docker build -t sanjaikumar1one/movie-rating:latest ."
    }
    stage("Push to Docker Hub") {
        withCredentials([usernamePassword(credentialsId: "docker-hub-login", passwordVariable: "PASS", usernameVariable: "USER")]) {
            bat "echo %PASS% | docker login -u %USER% --password-stdin"
            bat "docker push sanjaikumar1one/movie-rating:latest"
        }
    }
}