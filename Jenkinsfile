node('nodes'){
def mavenHome = tool name: "maven3.8.3"
	stage('pullthecode')
	{
		git branch: 'development', credentialsId: '9c1141a4-567e-44ab-a289-93a687040fe2', url: 'https://github.com/Sagar-a-8786/maven-web-application.git'
	}
	stage('build')
	{
		sh "$mavenHome/bin/mvn clean package"
	}
	stage('codecoverage')
	{
		sh "$mavenHome/bin/mvn clean sonar:sonar"
	}
	stage('artifactrepo')
	{
		sh "$mavenHome/bin/mvn clean deploy"
	}
	stage('deploy')
	{
		sshagent(['3fda235a-827e-48d5-85fc-55169f7b0b74']) {
    		sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/pipeline-scriptedway/target/maven-web-application.war ec2-user@13.233.93.69:/opt/apache-tomcat-9.0.54/webapps"
	}
	}
	stage('emailnotification')
	{
		emailext body: '''build complete

		regards,
		Sagar''', subject: 'build complete', to: 'sagaranand1234567@gmail.com,sagaranand0123456789@gmail.com'
	}
}
