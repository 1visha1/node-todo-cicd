pipeline {
	agent any
	stages {
		stage("code"){
			steps{
				git url: "https://github.com/1visha1/node-todo-cicd.git", branch: "master"
				echo "copy code"
			}
		}
		stage("build & test"){
			steps{
				sh "docker build -t node-app-test-new ."
				echo "building docker image and testig"
			}
		}
		stage("scan image"){
			steps{
				echo "image scan"
			}
		}
		
		stage("push image"){
			steps{
				withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"DP",usernameVariable:"DU" )]){
					sh "docker tag node-app:latest ${env.DU}/node-app-test-new:latest"
					sh "docker login -u ${env.DU} -p ${env.DP}"
					sh "docker push ${env.DU}/node-app-test-new:latest"
					echo "image uploading on docker hub"
				}
			}
		}
		stage("deploy"){
			steps{
				sh "docker-compose down && docker-compose up -d"
				echo "deploing app"
				
			}
		}
	}
}
