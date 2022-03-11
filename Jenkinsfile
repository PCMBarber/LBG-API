pipeline {
	agent any
	stages{
		stage('Build Image'){
			steps{
			sh 'docker build -t gcr.io/lbg-210222/api-piers:latest -t gcr.io/lbg-210222/api-piers:build-$BUILD_NUMBER .'
			}
		}
		stage('Push GCR'){
			steps{
            sh 'docker push gcr.io/lbg-210222/api-piers:build-$BUILD_NUMBER gcr.io/lbg-210222/api-piers:latest'
			}
		}
		stage('Reapply '){
			steps{
			sh '''kubectl apply -f ./kubernetes/nginx.yaml
            kubectl apply -f ./kubernetes/api-deployment.yml
			'''
			}
		}
        stage('Cleanup'){
			steps{
            sh 'docker system prune -f'
			}
		}
    }
}