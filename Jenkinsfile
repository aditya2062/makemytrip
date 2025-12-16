pipeline {

    agent any

    options {
        buildDiscarder(logRotator(numToKeepStr: '3', artifactNumToKeepStr: '3'))
    }

    tools {
        maven 'maven_3.9.11'
    }

    stages {
        stage('Code Compilation') {
            steps {
                echo 'Starting Code Compilation...'
                sh 'mvn clean compile'
                echo 'Code Compilation Completed Successfully!'
            }
        }
        stage('Code QA Execution') {
            steps {
                echo 'Running JUnit Test Cases...'
                sh 'mvn clean test'
                echo 'JUnit Test Cases Completed Successfully!'
            }
        }
        stage('Code Package') {
            steps {
                echo 'Creating WAR Artifact...'
                sh 'mvn clean package'
                echo 'WAR Artifact Created Successfully!'
            }
        }
    }
}



node {

    // Build Discarder
    properties([
        buildDiscarder(
            logRotator(numToKeepStr: '3', artifactNumToKeepStr: '3')
        )
    ])

    // Use Maven Tool
    def mvnHome = tool 'maven_3.9.11'
    env.PATH = "${mvnHome}/bin:${env.PATH}"

    stage('Code Compilation') {
        echo 'Starting Code Compilation...'
        sh "${mvnHome}/bin/mvn clean compile"
        echo 'Code Compilation Completed Successfully!'
    }

    stage('Code QA Execution') {
        echo 'Running JUnit Test Cases...'
        sh "${mvnHome}/bin/mvn clean test"
        echo 'JUnit Test Cases Completed Successfully!'
    }

    stage('Code Package') {
        echo 'Creating WAR Artifact...'
        sh "${mvnHome}/bin/mvn clean package"
        echo 'WAR Artifact Created Successfully!'
    }
}