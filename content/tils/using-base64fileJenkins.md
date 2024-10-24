+++
title = "File Parameters in Jenkins Pipeline"
date = 2024-10-24T09:57:55+05:30
type = "post"
description = "Using File Parameter in a Jenkins Pipeline"
in_search_index = true
[taxonomies]
tags = ["CICD","Jenkins","Automation"]
+++
# Using File Parameters in Jenkins Pipeline

Today, I was working on a Jenkins Pipeline that required handling a SQL dump file for our development environment. During this process, I encountered an important limitation: the default **file parameter** in Jenkins does not work with pipeline jobs; it only functions in **Freestyle Project** jobs.

To access file parameters in a Jenkins Pipeline, you need to use a plugin.

## Using the Base64FileParameter Plugin

The **Base64FileParameter** plugin allows you to access and handle file parameters within your pipeline seamlessly. This is essential for tasks where file uploads are required.

You can install the plugin using the following link:

**Plugin Link:** [File Parameters Plugin](https://plugins.jenkins.io/file-parameters/)

### Example Code

Here’s a simple example demonstrating how to use the Base64FileParameter in your Jenkins Pipeline:

```groovy
pipeline {
    agent any
    
    parameters {
        base64File(description: 'Upload a file', name: 'FILE')
    }

    stages {
        stage('Process File') {
            steps {
                script {
                    withFileParameter('FILE') {
                        sh 'cat ${FILE}' // Example command to read the file
                    }
                }
            }
        }
    }
}


