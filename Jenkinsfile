#!/usr/bin/env groovy

pipeline {
    agent {
        label 'os:linux && terraform'
    }
    options {
        skipDefaultCheckout()
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
    parameters {
        string(name: 'RELEASE_VERSION',
            defaultValue: '',
            description: 'The version of the terraform provider. (MAJOR.MINOR.PATCH, e.g. 0.0.1). If the version is left empty, release stage will be skipped.',
            trim:true)
    }
    stages {
        stage("Checkout") {
            steps {
                checkout scm
            }
        }
        stage("Release") {
            when {
                expression {
                    params.RELEASE_VERSION != ''
                }
            }
            steps {
                terraformProviderRelease(releaseVersion: params.RELEASE_VERSION)
            }
        }
    }
}
