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
    }
}
