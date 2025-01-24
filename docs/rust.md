```shell
pipeline {
    agent any

    stages {
        stage('clone') {
            steps {
               git 'https://gitee.com/liufeihua/salvo-admin.git'
            }
        }
        stage('install') {
            steps {
                sh 'ls'
                sh '/root/.cargo/bin/cargo build'
            }
        }

        
    }
}
```