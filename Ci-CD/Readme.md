## Jenkins Workflow
###   Jenkins password reset
- systemctl stop jenkins 
- vim /var/lib/jenkins/config.xml
 - rewrite replace to `<useSecurity>false</useSecurity>`
- systemctl start jenkins
#### Parameters base script
```
pipeline{
    agent any
    parameters{
        string(name: 'STRING_PARAM', defaultValue: 'default Value', description: 'ENter your a string')
        booleanParam(name: 'BOOL_PARAM', defaultValue: false, description: 'Enable or disable something')
        choice(name: 'CHOICE_PARAM', choices: ['Option 1', 'Option 2', 'Option 3'], description: 'Choose an option')
        password(name: 'PASSWORD_PARAM', defaultValue: '', description: 'Enter a password')
        text(name: 'TEXT_PARAM', defaultValue: '', description: 'Enter a multi-line text')
        file(name: 'FILE_PARAM', description: 'Upload a file')
        text(name: 'FILE_PARAM', defaultValue: '', description: 'Enter a multi-line text')
        
    }
    stages{
        stage('Display Parameters'){
            steps{
                echo "String Parameter: ${params.STRING_PARAM}"
                echo "Boolean Parameter: ${params.BOOL_PARAM}"
                echo "Choice Parameter: ${params.CHOICE_PARAM}"
                echo "Password Parameter: ${params.PASSWORD_PARAM}"
                echo "Text Parameter: ${params.TEXT_PARAM}"
                echo "File Parameter: ${params.FILE_PARAM}"
            }
        }
    }
}

``` 
## Mail server configuration
- First install the Email Extension Plugin in Jenkins.
- Go to manage jenkins > configure system > Extended E-mail Notification > SMTP server > Add SMTP server > fill the form > save
- Add the following code in the pipeline script
- Go to gmail and enable less secure app access.
```
post {
	always {
		script {
			def jobName = env.JOB_NAME
			def buildNumber = env.BUILD_NUMBER
			def pipelineStatus = currentBuild.result ?: 'UNKOWN'
			def bannerColor = pipelineStatus.toUppercase() == 'SUCCESS' ? 'green' : 'red'
			def body = """
			<html>
			<body>
			<div style = "border:4px solid ${bannerCOlor}; padding: 10px;">
			<h2> ${jobName} - Build ${buildNumber}</h2>
			<div style = "background-color: ${bannerColor}; padding: 10px;">
			<h3 style="color: white;"> pipeline status: ${pipelineStatus.toUppercase()}</h3>
			</div>
			<p> Check the <a href="{BUILD_URL}"> console output </a>.</p>
			</div>
			</body>
			</html>
		"""
		emailest ( 
			subject: "${jobName} - Build ${buildNumber} - ${pipelineStatus.toUppercase()}"
			body: body,
			to: 'mamunurr191@gmail.com',
			from: 'mamunurrashid148@gmail.com',
			replyTo: 'mamunurrashid148@gmail.com',
			mimeType: 'text/html',
			
		}
	}
}
```
## Git Action 
-   `core concepts`: workflow->Job->step->action
-  `Triggers`: `on:push`, `on:pull_request`, `on:workflow_dispatch`, `on: schedule`
- `Runner`: `ubuntu-latest`, `windows-latest`, `macos-latest`
- `Jobs`: `name`, `runs-on`, `steps`
- `Steps`: `name`, `uses`, `run`, `with`, `env`
- `Actions`: `checkout`, `setup-node`, `npm install`, `npm run build`, `deploy`
- `Secrets`: `GITHUB_TOKEN`, `NPM_TOKEN`

- Git Action on Build 
```bash
name: Build and Push Docker Image
        uses: mr-smithers-excellent/docker-build-push@v4
        with:
          image: mamunurrashid123/my-project
          registry: docker.io
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}
```
- Git Action on Deploy 
- Link https://github.com/marketplace/actions/ssh-remote-commands