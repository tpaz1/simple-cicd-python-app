// Jenkinsfile (Declarative Pipeline)
// Global Variable goes here
// Pipeline block
pipeline {
// Agent block
agent {
   node {
      label 'master'
   }
}
options {
   buildDiscarder(logRotator(numToKeepStr: '5'))
   timestamps()
}
parameters {
   string(name: "Branch_Name", defaultValue: 'main', description: 'A name of the Git branch that contain the jenkinfile code')
   string(name: "Image_Name", defaultValue: 'tom-check', description: 'A name of the image that you want to build')
   string(name: "Image_Tag", defaultValue: 'latest', description: 'Image tag')
   
   booleanParam(name: "PushImage", defaultValue: true)
}
// Stage Block
stages {// stage blocks
   stage("Build docker images") {
      steps {
         script {
            echo "Bulding docker images"
            def buildArgs = """ ."""
            docker.build("${params.Image_Name}:${params.Image_Tag}", buildArgs)
         }
     }
}
stage("Push to Dockerhub") {
   when {
      equals expected: "true", actual: "${params.PushImage}"
   }
   steps {
      script {
         echo "Pushing the image to docker hub"
         def localImage = "${params.Image_Name}:${params.Image_Tag}"
         def repositoryName = "tpaz1/${localImage}"
         sh "docker tag ${localImage} ${repositoryName} "
         docker.withRegistry("", "dockerhub") {
            def image = docker.image("${repositoryName}");
            image.push()
         }
     }
  }
}}
post {
   always {
      script {
         echo "I am execute always"
      }
   }
   success {
      script {
         echo "I am execute on success"
      }
   }
   failure {
      script {
         echo "I am execute on failure"
      }
   }
}}
