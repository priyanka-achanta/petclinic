node
{
		def build_ok = true
		
        notify('Started')
		
        stage('checkout') {
                git 'https://github.com/priyanka-achanta/petclinic.git'
        }

        stage('Build') {
                sh 'mvn clean package'
        }
		
		try {
        stage('Archive1') {
                archiveArtifacts 'target/*.jar'
        }
		}
		catch (err)
		{
				build_ok = false
				notify("Error ${err}")
				echo e.toString()
				echo 'archival'
				currentBuild.result = 'FAILURE'
		}		
		
		
        stage('Test Results') {
                junit 'target/surefire-reports/*.xml'
        }
        notify('Success')
		
		
		if(build_ok) {
				currentBuild.result = "SUCCESS"
		} else {
				currentBuild.result = "FAILURE"
		}
}

def notify(status){
    emailext (
      to: "priyanka.vishnubhatla@gmail.com",
      subject: "${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: """<p>${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at <a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a></p>""",
    )
}
