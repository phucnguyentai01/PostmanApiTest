pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh label: 'API Collection Tests', script: 'newman run "Collections/Searching_City_Collection.postman_collection.json" -e "Environments/Searching_City_Environment.postman_environment.json" -d Resources/Example_API_Test_Data.csv --reporters cli,junit,htmlextra --reporter-junit-export "newman/report.xml" --reporter-htmlextra-export "newman/report.html" --suppress-exit-code'
                // publish html
                publishHTML target: [
                    allowMissing: false,
                    alwaysLinkToLastBuild: false,
                    keepAll: true,
                    reportDir: 'coverage',
                    reportFiles: 'newman/report.html',
                    reportName: 'HTML Report'
                  ]
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}