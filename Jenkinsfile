pipeline {
 agent any
   stages {
	stage('gcloud auth') {
            steps {
                withCredentials([file(credentialsId: 'JENKINS-ID', variable: 'JENKINS_KEY_FILE')]) {
			sh """
                               gcloud version
			       gcloud auth activate-service-account --key-file="$JENKINS_KEY_FILE"
                               gcloud auth configure-docker us-docker.pkg.dev
			   """
			}
            }
      }
       stage('image promotion') {
            steps {
		sh """
                    docker pull haribabup279/&{image_to_promote}
                    docker tag haribabup279/&{image_to_promote}  us-docker.pkg.dev/hari-cloud-first-project/gcr-images-registry/&{image_to_promote}
                    docker push us-docker.pkg.dev/hari-cloud-first-project/gcr-images-registry/&{image_to_promote}
		"""
            }
      }
   }
}
