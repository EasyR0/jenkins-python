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

                "C:\\Users\\User\\AppData\\Roaming\\npm\\pm2.cmd" delete greetings-app-dev & EXIT /B 0
                "C:\\Users\\User\\AppData\\Roaming\\npm\\pm2.cmd" start app.py --name greetings-app-dev --interpreter venv\\Scripts\\python.exe -- --port 7001
                "C:\\Users\\User\\AppData\\Roaming\\npm\\pm2.cmd" list
                '''
            }
        }
    }
}
