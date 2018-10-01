#!/usr/bin/groovy

import java.text.SimpleDateFormat

pipeline {
    agent {
        kubernetes {
            cloud "kubernetes"
            label "go-demo-cicd-k8s-1-build"
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
        stage('Build') {
            steps {
                echo 'Build Step'
                container("golang") {
                    script {
                         // Change Build Name Ex: #18 to #18.10.01-18
                        currentBuild.displayName = new SimpleDateFormat("yy.MM.dd").format(new Date()) + "-${env.BUILD_NUMBER}"
                    }
                    k8sBuildGolang("go-demo")
                }

                container("docker") {
                  k8sBuildImageBeta(image, false)
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Test Step'
            }
        }
        stage('Sonar') {
            steps {
                echo 'Sonar Step'
            }
        }
        stage('Versionate') {
            steps {
                echo 'Versionate Step'
            }
        }
        stage('Bake') {
            steps {
                echo 'Bake Step'
            }
        }
        stage('Contract') {
            steps {
                echo 'Contract Step'
            }
        }
        stage('Store') {
            steps {
                echo 'Store Step'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy Step'
            }
        }
    }
}
