pipeline {
  agent any

  triggers {
    githubPush()
  }

  stages {
    stage('Install Chrome and chromedriver') {
      agent { label 'chrome' }
      
      steps {
        sh 'sudo apt-get update && sudo apt-get install -y curl unzip xvfb libxi6 libgconf-2-4'
        sh 'curl -sS -o - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add'
        sh 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" | sudo tee /etc/apt/sources.list.d/google-chrome.list'
        sh 'sudo apt-get update && sudo apt-get install -y google-chrome-stable'
        sh 'curl -sS -o chromedriver.zip https://chromedriver.storage.googleapis.com/LATEST_RELEASE'
        sh 'curl -sS -o chromedriver_linux64.zip https://chromedriver.storage.googleapis.com/`cat chromedriver.zip`/chromedriver_linux64.zip'
        sh 'unzip chromedriver_linux64.zip'
        sh 'chmod +x chromedriver'
        sh 'sudo mv chromedriver /usr/local/bin'
      }
    }
  }
}
