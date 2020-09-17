pipeline{
    agent any
    stages{

        // Stage 1 Create a Kubernetes Cluster
        stage('Create kubernetes cluster') {
			steps {
				withAWS(region:'us-west-2', credentials:'aws_credentials') {
					sh '''
						eksctl create cluster \
						--name microservicesCluster \
						--version 1.17 \
						--nodegroup-name standard-workers \
						--node-type t2.small \
						--nodes 2 \
						--nodes-min 1 \
						--nodes-max 3 \
						--node-ami auto \
						--region us-west-2 \
						--zones us-west-2a \
						--zones us-west-2b \
						--zones us-west-2c \
					'''
				}
			}
		}

        // Stage 2 Create a Config file
        stage('Create config file cluster') {
			steps {
				withAWS(region:'us-west-2', credentials:'aws_credentials') {
					sh '''
						aws eks --region us-west-2 update-kubeconfig --name microservicesCluster
					'''
				}
			}
		}


    }
}