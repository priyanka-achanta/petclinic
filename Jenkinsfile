node
{
	notify('Started')
	
	stage('checkout') {
		git 'https://github.com/priyanka-achanta/petclinic.git'
	}

	stage('Build') {
		sh 'mvn clean package'
	}
	stage('Archive1') {
		archiveArtifacts 'target/*.war'
	}
	stage('Test Results') {
		junit 'target/surefire-reports/*.xml'
	}
	notify('Success')
}

def notify(status){
    emailext (
      to: "priyanka.vishnubhatla@gmail.com",
      subject: "${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: """<p>${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at <a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a></p>""",
    )
}
