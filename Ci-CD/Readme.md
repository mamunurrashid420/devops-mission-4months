## Jenkins Workflow
###   Jenkins password reset
- systemctl stop jenkins 
- vim /var/lib/jenkins/config.xml
 - rewrite replace to `<useSecurity>false</useSecurity>`
- systemctl start jenkins
#### Parameters base script

-  
