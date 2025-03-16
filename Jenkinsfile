pipeline {
    agent any
    stages {
        stage('Git Checkout') {
            steps {
                sh 'python -m py_compile sources/add2vals.py sources/calc.py' 
                stash(name: 'compiled-results', includes: 'sources/*.py*') 
            }
        }


    }

}
