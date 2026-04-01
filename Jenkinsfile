pipeline {
    agent any

    stages {
        stage('install-pip-deps') {
            steps {
                echo 'Installing all required dependencies...'
                bat '''
                if exist python-greetings rmdir /s /q python-greetings
                git clone https://github.com/mtararujs/python-greetings.git

                cd python-greetings
                "C:\\Users\\User\\AppData\\Local\\Python\\bin\\python.exe" -m venv venv
                venv\\Scripts\\python.exe -m pip install -r requirements.txt
                '''
            }
        }

        stage('deploy-to-dev') {
            steps {
                echo 'Deploying to dev...'
                bat '''
                if exist python-greetings rmdir /s /q python-greetings
                git clone https://github.com/mtararujs/python-greetings.git

                cd python-greetings
                "C:\\Users\\User\\AppData\\Local\\Python\\bin\\python.exe" -m venv venv
                venv\\Scripts\\python.exe -m pip install -r requirements.txt

                pm2 delete greetings-app-dev & set "errorlevel=0"
                pm2 start app.py --name greetings-app-dev --interpreter venv\\Scripts\\python.exe -- --port 7001
                '''
            }
        }
    }
}
