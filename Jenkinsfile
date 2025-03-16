pipeline {
    agent any
    stages {
        stage('Git Checkout') {
            steps {
                sh 'python3 -m py_compile sources/add2vals.py sources/calc.py' 
                stash(name: 'compiled-results', includes: 'sources/*.py*') 
            }
        }
        stage('Test') {
            steps {
                sh 'py.test --junit-xml test-reports/results.xml sources/test_calc.py'
            }
            post {
                always {
                    junit 'test-reports/results.xml'
                }
            }
        }
        stage('Deliver') { 
            steps {
                sh "python3 -m venv myenv"
                sh "source myenv/bin/activate"
                sh "pip install pyinstaller"
                sh "echo pyinstall --version"
                sh "pyinstaller --onefile sources/add2vals.py" 
                sh "deactivate"
            }
            post {
                success {
                    archiveArtifacts 'dist/add2vals' 
                }
            }
        }

    }

}
