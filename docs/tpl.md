
```shell
pipeline {
    agent any

    stages {
        stage('clone') {
            steps {
                git branch: '3.0', url: 'https://gitee.com/liufeihua/spring-cloud-tpl.git'
            }
        }
        stage('build eureka') {
            steps {
                sh '''
                cd tpl-eureka
                /root/gradle-8.2.1/bin/gradle build
                cp deploy/tpl-eureka.sh build/libs/ 
                chmod +x build/libs/tpl-eureka.sh
                '''
                 
            }
        }
        stage('stop eureka') {
            steps {
                sh 'cd tpl-eureka/build/libs && ./tpl-eureka.sh stop'
            }
        }
        stage('start eureka') {
            steps {
                withEnv(['JENKINS_NODE_COOKIE=dontkillme]']) {
                    sh '''
                        cd tpl-eureka/build/libs
                         ./tpl-eureka.sh start

                    '''
                }
            }
        }
        stage('eureka status') {
            steps {
                sh 'cd tpl-eureka/build/libs && ./tpl-eureka.sh status'
            }
        }
        stage('build system') {
            steps {
                sh '''
                cd tpl-system
                /root/gradle-8.2.1/bin/gradle build
                cp deploy/tpl-system.sh build/libs/ 
                chmod +x build/libs/tpl-system.sh
                '''
                 
            }
        }
        stage('stop system') {
            steps {
                sh 'cd tpl-system/build/libs && ./tpl-system.sh stop'
            }
        }
        stage('start system') {
            steps {
                withEnv(['JENKINS_NODE_COOKIE=dontkillme]']) {
                    sh '''
                        cd tpl-system/build/libs
                         ./tpl-system.sh start
                    '''
                }
            }
        }
        stage('system status') {
            steps {
                sh 'cd tpl-system/build/libs && ./tpl-system.sh status'
            }
        }

        stage('build gateway') {
            steps {
                sh '''
                cd tpl-gateway
                /root/gradle-8.2.1/bin/gradle build
                cp deploy/tpl-gateway.sh build/libs/ 
                chmod +x build/libs/tpl-gateway.sh
                '''
                 
            }
        }
        stage('stop gateway') {
            steps {
                sh 'cd tpl-gateway/build/libs && ./tpl-gateway.sh stop'
            }
        }
        stage('start gateway') {
            steps {
                withEnv(['JENKINS_NODE_COOKIE=dontkillme]']) {
                    sh '''
                        cd tpl-gateway/build/libs
                         ./tpl-gateway.sh start

                    '''
                }
            }
        }
        stage('gateway status') {
            steps {
                sh 'cd tpl-gateway/build/libs && ./tpl-gateway.sh status'
            }
        }
    }
}
```