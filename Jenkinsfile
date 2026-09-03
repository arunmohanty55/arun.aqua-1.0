pipeline{
    agent any
      stages{
          stage ('clone the code from repo'){
              steps {
                  git url: "https://github.com/arunmohanty55/arun.aqua-1.0.git", branch: 'master'
              }
          }
          stage ('build the code') {
              steps {
                  sh 'docker build -t arun-aqua:1.0 .'
              }
          }
              stage ('test'){
                  steps{
                      echo "testing"
                  }
              }
              stage ('deploy'){
                  steps{
                     sh 'docker run -d -p 5000:5000 --name arun-aqua arun-aqua:1.0'
                  }
              }
          }
      }
