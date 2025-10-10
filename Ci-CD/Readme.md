## Jenkins Workflow
###   Jenkins password reset
- systemctl stop jenkins 
- vim /var/lib/jenkins/config.xml
 - rewrite replace to `<useSecurity>false</useSecurity>`
- systemctl start jenkins
#### Parameters base script
```
parameters{
    string(name: 'STRING_PARAM', defaultValue: 'default Value', description: 'ENter your a string')
    booleanParam(name: 'BOOL_PARAM', defaultValue: false, description: 'Enable or disable something')
    choice(name: 'CHOICE_PARAM', choices: ['Option 1', 'Option 2', 'Option 3'], description: 'Choose an option')
    password(name: 'PASSWORD_PARAM', defaultValue: '', description: 'Enter a password')
    text(name: 'TEXT_PARAM', defaultValue: '', description: 'Enter a multi-line text')
    file(name: 'FILE_PARAM', description: 'Upload a file')
    
}

``` 
