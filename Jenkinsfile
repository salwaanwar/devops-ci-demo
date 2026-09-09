stage('Build') {
    steps {
        echo 'Building application...'
        bat '"C:\Users\habib\AppData\Local\Programs\Python\Python314\python.exe" -m py_compile app.py'
    }
}

stage('Test') {
    steps {
        echo 'Running automated tests...'
        bat '"C:\Users\habib\AppData\Local\Programs\Python\Python314\python.exe" -m pytest -v'
    }
}
