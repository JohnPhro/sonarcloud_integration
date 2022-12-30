pipeline {
  agent any
  tools { 
        maven 'Maven_3_5_2'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=johnapp2 -Dsonar.organization=johnapp2 -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=6398f9bec14949dc4cdeb66d47f29aa953cd6526'
			}
    }

	stage('RunSCAAnalysisUsingSnyk') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
    }	

// // building docker image
// stage('Build') { 
//             steps { 
//                withDockerRegistry([credentialsId: "dockerlogin", url: ""]) {
//                  script{
//                  app =  docker.build("tech365image")
//                  }
//                }
//             }
//     }

// 	stage('Push') {
//             steps {
//                 script{
//                     docker.withRegistry("https://924338258393.dkr.ecr.us-east-2.amazonaws.com", "ecr:us-east-2:aws-credentials") 
// 			{
//                     app.push("latest")
//                     }
//                 }
//             }
//     	}


  }
}
