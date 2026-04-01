pipeline {
    agent any

    stages {
        stage('install-pip-deps') {
            steps {
                echo 'Installing all required dependencies...'
                installDeps()
            }
        }

        stage('deploy-to-dev') {
            steps {
                echo 'Deploying to dev...'
                deployApp('dev', '7001')
            }
        }

        stage('tests-on-dev') {
            steps {
                echo 'Testing dev...'
                runTests('dev')
            }
        }

        stage('deploy-to-stg') {
            steps {
                echo 'Deploying to stg...'
                deployApp('stg', '7002')
            }
        }

        stage('tests-on-stg') {
            steps {
                echo 'Testing stg...'
                runTests('stg')
            }
        }

        stage('deploy-to-preprod') {
            steps {
                echo 'Deploying to preprod...'
                deployApp('preprod', '7003')
            }
        }

        stage('tests-on-preprod') {
            steps {
                echo 'Testing preprod...'
                runTests('preprod')
            }
        }

        stage('deploy-to-prod') {
            steps {
                echo 'Deploying to prod...'
                deployApp('prod', '7004')
            }
        }

        stage('tests-on-prod') {
            steps {
                echo 'Testing prod...'
                runTests('prod')
            }
        }
    }
}

def installDeps() {
    bat '''
    if exist python-greetings rmdir /s /q python-greetings
    git clone https://github.com/mtararujs/python-greetings.git

    cd python-greetings
    "C:\\Users\\User\\AppData\\Local\\Python\\bin\\python.exe" -m venv venv
    venv\\Scripts\\python.exe -m pip install -r requirements.txt
    '''
}

def deployApp(envName, port) {
    bat """
    if exist python-greetings rmdir /s /q python-greetings
    git clone https://github.com/mtararujs/python-greetings.git

    cd python-greetings
    "C:\\Users\\User\\AppData\\Local\\Python\\bin\\python.exe" -m venv venv
    venv\\Scripts\\python.exe -m pip install -r requirements.txt

    "C:\\Users\\User\\AppData\\Roaming\\npm\\pm2.cmd" delete greetings-app-${envName} & EXIT /B 0
    "C:\\Users\\User\\AppData\\Roaming\\npm\\pm2.cmd" start app.py --name greetings-app-${envName} --interpreter venv\\Scripts\\python.exe -- --port ${port}
    "C:\\Users\\User\\AppData\\Roaming\\npm\\pm2.cmd" list
    """
}

def runTests(envName) {
    bat """
    if exist tests rmdir /s /q tests
    git clone https://github.com/mtararujs/course-js-api-framework.git tests

    cd tests
    npm install
    npm run greetings greetings_${envName}
    """
}
