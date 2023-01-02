//******************
// Note: The following is the actual jenkins file for Linux.
// We should use Linux and the following jenkins file in real life pipelines
// pipeline {
//     agent none
//     stages {
//         stage('Build Jar') {
//             agent {
//                 docker {
//                     image 'maven:3-alpine'
//                     args '-v $HOME/.m2:/root/.m2' // to speed up for further runs
//                 }
//             }
//             steps {
//                 sh 'mvn clean package -DskipTests'
//             }
//         }
//         stage('Build Image') {
//             steps {
//                 script {
//                 	app = docker.build("mustafasdet/se-docker")
//                 	    // This will be name of our built image
//                 }
//             }
//         }
//         stage('Push Image') {
//             steps {
//                 script {
// 			        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
//                                         // dockerhub is the credential id we added in the jenkins
// 			        	app.push("${BUILD_NUMBER}")
// 	// build_number: jenkins has build number and we use that one to know the version with this tag
// 			            app.push("latest")
// 			        }
//                 }
//             }
//         }
//     }
// }


pipeline {
    // master executor should be set to 0 - I have done already
    // I am using my mac as jenkins-slave and it has docker and maven installed
    // So we skip adding maven to our agent
    agent any
    stages {
        stage('Build Jar') {
            steps {
                //bat => for windows
                sh "mvn clean package -DskipTests"
            }
        }
        stage('Build Image') {
            steps {
                //bat => for windows
                sh "docker build -t=mustafasdet/se-docker ."
            }
        }
        stage('Push Image') {
            steps {
			    withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'Math4632.', usernameVariable: 'mustafasdet')]) {
                    //bat => for windows
			        sh "docker login --username=${user} --password=${pass}"
			        sh "docker push mustafasdet/se-docker:latest"
			    }
            }
        }
    }
}