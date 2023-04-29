pipeline	{
	agent any
	tools	{
		maven 'maven-3.9.1'
	}
	stages	{
		stage("Build jar")	{
			steps	{
				script	{
					echo 'Building the application.....'
					sh 'mvn package'
				}
			}
		}
		stage("Build docker image")	{
			steps	{
				script	{
					echo 'Building the docker image.....'
					withCredentials([usernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')])	{
						sh 'docker build -t surajdubey08/demo-java-maven-app:jma-2.0 .'
						sh "echo $PASS | docker login -u $USER --password-stdin"
						sh ' docker push surajdubey08/demo-java-maven-app:jma-2.0'
					}
				}
			}
		}
		stage("Deploy the Artifact")	{
			steps	{
				script	{
					echo "Deploying the artifact......."
				}
			}
		}
	}
}
