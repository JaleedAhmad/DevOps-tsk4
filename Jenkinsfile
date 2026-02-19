pipeline {
    agent any

    stages {
        stage('Hello World Verification') {
            steps {
                echo 'Hello World! The webhook successfully triggered the pipeline.'
            }
        }
        stage('Setup Environment') {
            steps {
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Deploy App') {
            steps {
                sh '''
                    pkill -f "python3 app.py" || true
                    sleep 2
                    . venv/bin/activate
                    
                    # Prevent Jenkins from killing the app
                    export JENKINS_NODE_COOKIE=dontKillMe
                    
                    nohup python3 app.py > flask_app.log 2>&1 &
                    echo "Application deployed to port 3000!"
                '''
            }
        }
    }
}
