pipeline {
    agent any
     environment {
                    version0 = sh(returnStdout: true, script: 'echo `aws s3api list-object-versions --bucket ml-models-bucket-345  --prefix ml_model.py --query "Versions[0].[VersionId]"  --output text`'  )
                    version1 = sh(returnStdout: true, script: 'echo `aws s3api list-object-versions --bucket ml-models-bucket-345  --prefix ml_model.py --query "Versions[1].[VersionId]"  --output text `' )
                }
    stages {
        stage('ServerlessDeploymentofMLModel') {
            steps {
                git branch: 'main', url: 'https://github.com/NokkuPrudhvi/Serverless-architecture-creation-and-model-deployment.git'
                sh 'echo ${version0}'
                sh 'aws s3api get-object --bucket ml-models-bucket-345 --key ml_model.py  ml_model --version-id ${version0}'
                sh 'aws s3api get-object --bucket ml-models-bucket-345 --key ml_model.py  ml_model_previous_version --version-id ${version1}' 
                sh 'sls deploy'
                }
        }
    }
}
