

```groovy

pipeline {
    agent { 
        node {
            label 'docker-node-sfdx'
            }
      }
    stages {
        stage('CodeScan') {
            steps {
                echo "Scanning the code with PMD.."
                sh '''
                echo "doing PMD  Scan..."
                '''
            }
        }
        stage('BuildCheckOnly') {
            steps {
                echo "Buliding with CheckOnly"
                sh '''
                echo "Building Checkonly..."
                '''
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy....'
                sh '''
                echo "Deploying..."
                '''
            }
        }
    }
}
```



## References
- [ Learn Jenkins! Complete Jenkins Course - Zero to Hero ](https://www.youtube.com/watch?v=6YZvp2GwT0A)
- [Cron Format](https://cloud.google.com/scheduler/docs/configuring/cron-job-schedules#:~:text=next%20scheduled%20time.-,Cron%20job%20format,API%20to%20set%20your%20schedule.)