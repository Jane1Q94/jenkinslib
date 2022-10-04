@Library('jenkinslib') _

def tools = new yangjijian.tools()

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
                        tools.PrintColorMsg("获取代码", "green")
                    }
                }
            }
        }
        stage("Build"){
            steps{
                timeout(time: 1, unit: "MINUTES"){
                    script{
			tools.PrintColorMsg("编译代码", "green1")
                    }
                }
            }
        }
        stage("Sonar"){
            steps{
                timeout(time:1, unit: "MINUTES"){
                    script{
                        tools.PrintColorMsg("代码扫描", "blue")
                        node = tool "node"
                        tools.PrintColorMsg("${node}", "red")
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
