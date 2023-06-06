pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout source code from a Git repository
                git credentialsId: '142c8a10-24eb-4811-8e6d-0c43d8decd01', url: 'https://github.com/DeepthiT-131/Angular_Test.git/'
            }
        }
        stage("Install npm Packages and Build "){
            steps {
                bat 'npm install'
                bat 'ng build'
            }
        }
       stage("Zip file"){
            steps {
                bat 'powershell Compress-Archive -Path "C:/ProgramData/Jenkins/.jenkins/workspace/UDPBuild/dist/test" -DestinationPath "D:/archive.zip"'
        }
    }
		stage("UnZip Files"){
			steps{
			bat 'powershell -Command "Expand-Archive -Path \'D:/archive.zip\' -DestinationPath \'D:/UDPFiles\'"' 
		}
	}
		stage('Move Files') {
                steps {
                    // Move files from source to destination by replacing the exixting files in existing folder.
                    bat 'robocopy "D:/UDPFiles/test" "D:/UDPNew" /E /IS /MOVE /R:1 /W:1'
                }
            }
}
}

