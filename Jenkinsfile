pipeline {
    agent {
        docker{ 
            image 'andressaroberts/rubywd'
        } 
    }
    
    stages {
        stage('Build'){
            steps {
                echo 'Building or Resolve Dependencies!'
                sh 'rm -f Gemfile.lock'
                sh 'bundle install'
            }
        }
        stage('Test'){
            steps {
                echo 'Running regression tests'
		        sh 'bundle exec cucumber -p ci'
            }
        }
        stage('UAT'){
            steps{
                echo 'Wait for user Acceptance'
                input (message: 'Go to production?', ok: 'Yes')
            }
        }
        stage('Prod'){
            steps{
                echo 'WebApp is Ready :)'
            }
        }
    }
}
