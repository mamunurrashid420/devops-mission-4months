## Java project 
```jenkins
pipeline{
    agent any
    tools{
        maven 'maven3'
        jdk 'jdk8'
    }
    stages{
        stage('Git checkout'){
            steps{
                git 'https://github.com/username/repo.git'
            }   
        }
        stage('Build'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage('Test'){
            steps{
                sh 'mvn test'
            }
        }
        stage('Build'){
            steps{
                sh 'mvn package'
            }
        }
    }
}
```
### Parameters Base jenkins file
- First setup in jenkins 
- Go to `project is parameters` and add `string parameter` and name it `branch` and default value `main`
    - select Name `branch` and default value `main`
    - save
```bash
pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
               git branch:  "${params.Branch_name}", url: 'https://github.com/mamunurrashid420/FullStack-Blogging-App.git'
            }
        }
        stage("hello world"){
            steps {
                echo "hello world"
            }
        }
    }
}
```
pipeline {
    agent any
    parameters{
        choice (name: "Branch_name", choices: ['main','Dev','feature1'])
    }
    stages {
        stage('Git Checkout') {
            steps {
               git branch:  "${params.Branch_name}", url: 'https://github.com/mamunurrashid420/FullStack-Blogging-App.git'
            }
        }
        stage("hello world"){
            steps {
                echo "hello world"
            }
        }
    }
}

```