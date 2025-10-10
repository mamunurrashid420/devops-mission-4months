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
