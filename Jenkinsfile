pipeline {

    options {
        buildDiscarder(logRotator(numToKeepStr: '4', artifactNumToKeepStr: '0'))
        timestamps()
    }

    parameters {
        choice(name: 'IMAGE_NAME', choices: ['main-image', 
                                             'report-image', 
                                             'ce-image', 
                                             ], description: 'Provide image name')
        string(defaultValue: 'ami-0d1d03ecdc7b45103', name: "SOURCE_AMI", description: 'Provide source_ami id. ex.ami-0d1d03ecdc7b45103')
    }
        

    stages {
        stage('Build image') {
            steps {
                script {
                    sh(
                        label: 'Running packer build',
                        script: """
                        packer build \
                        -var "image_name=${IMAGE_NAME}" \
                        -var "ami=${SOURCE_AMI}" \
                        build-main-image
                        """
                    )
                }
            }
        }

        stage('Wipe out'){
            steps {
                cleanWs()
            }
        }

    }
}