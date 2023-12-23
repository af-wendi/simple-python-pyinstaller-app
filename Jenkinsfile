node {
    try {
        stage('Build') {
            // Menggunakan Docker image Python untuk build
            docker.image('python:3.12.1-alpine3.19').inside {
                // Langkah-langkah untuk build
                sh 'python -m py_compile sources/add2vals.py sources/calc.py'
                stash(name: 'compiled-results', includes: 'sources/*.py*')
            }
        }

        stage('Test') {
            // Menggunakan Docker image pytest untuk pengujian
            docker.image('qnib/pytest').inside {
                // Langkah-langkah untuk pengujian
                sh 'py.test --junit-xml test-reports/results.xml sources/test_calc.py'
            }
        }
    } catch (Exception e) {
        currentBuild.result = 'FAILURE'
        throw e
    } finally {
        // Post-build action: Menampilkan laporan JUnit
        junit 'test-reports/results.xml'
    }
}
