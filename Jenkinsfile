@Library('jenkinslib') _

def tools = new org.jenkinslib.tools()

pipeline {
    agent any
    options {
        timestamps()
        skipDefaultCheckout()
        disableConcurrentBuilds()
        timeout(time: 1, unit: "MINUTES")
    }
    parameters {
        string(name: "test2", defaultValue: "test2", description: "test2")
    }
    stages {
        stage('Get code') {
            when{
                environment name: "test", value: "abc"
            }
            steps {
                timeout(time:1, unit: "MINUTES"){
                    script{
                        print("Get Code")
                    }
                }
            }
        }
        stage("Build"){
            steps{
                timeout(time: 1, unit: "MINUTES"){
                    script{
			                  tools.PrintMsg(“this is my lib”)
                        print("Build")
                    }
                }
            }
        }
        stage("Sonar"){
            steps{
                timeout(time:1, unit: "MINUTES"){
                    script{
                        println("Sonar Scan")
                        node = tool "node"
                        print("${node}")
                        sh "${node}/node --version"
                        input id: '1', message: '是否要继续？', ok: 'yes', parameters: [string(defaultValue: 'test default value', description: 'test description', name: 'test input')], submitter: 'yangjijian'
                    }
                }
            }
        }
    }
    post{
        success {
            script{
                currentBuild.description="构建成功"
                println("${test}")
                println(env)
            }
        }
    }
}
