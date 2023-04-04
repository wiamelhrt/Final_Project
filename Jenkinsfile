pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                checkout scm
            }
        }
        
        stage('kubeflow pipeline') {
            steps {
                bat 'python kubeflow.py'
               
            }
        }
      stage('deploy') {
            steps {
                
                bat 'python -m pip install uvicorn'
                bat 'start cmd /c "python -m uvicorn app:app --reload & echo %PROCESS_ID% > pid.txt"'
            }
        }
        stage('Stop Uvicorn') {
            
            steps {
                bat 'set /p pid=<pid.txt && timeout /t 60 && taskkill /f /pid %pid%'
                
            }
        }
    }
}



