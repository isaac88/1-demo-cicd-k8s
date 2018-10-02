#!/usr/bin/groovy

import java.text.SimpleDateFormat

pipeline {
    agent {
        kubernetes {
            cloud "kubernetes"
            label "go-demo-cicd-k8s-1-build"
            serviceAccount "tiller"
            yamlFile "KubernetesPod.yaml"
        }
    }
    environment {
        image = "isaac88/go-demo-cicd-k8s-1-build"
        project = "go-demo-cicd-k8s-1"
        domain = "54.76.149.175.nip.io"
        cmAddr = "cm.54.76.149.175.nip.io"
    }
    stages {
        stage('build') {
            steps {
                container("golang") {
                    script {
                         // Change Build Name Ex: #18 to #18.10.01-18
                        currentBuild.displayName = new SimpleDateFormat("yy.MM.dd").format(new Date()) + "-${env.BUILD_NUMBER}"
                    }
                    // Build the code
                    k8sBuildGolang("go-demo")
                }
                // Build a docker image with the compiled code and push to docker registry
                container("docker") {
                  k8sBuildImageBeta(image, false)
                }
            }
        }
        stage("func-test") {
            steps {
                container("helm") {
                    k8sUpgradeBeta(project, domain, "--set replicaCount=2 --set dbReplicaCount=1")
                }
                container("kubectl") {
                    k8sRolloutBeta(project)
                }
                container("golang") {
                    k8sFuncTestGolang(project, domain)
                }
            }
          post {
            always {
                container("helm") {
                    k8sDeleteBeta(project)
                }
            }
          }
        }
    }
}
