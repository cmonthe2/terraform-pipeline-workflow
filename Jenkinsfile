pipeline {
    agent any

    stages {
        stage('git clone') {
            steps {
               checkout([$class: 'GitSCM', branches: [[name: '**']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/cmonthe2/terraform_1.git']]])
            }
        }
        
        stage('terraform init') {
            steps {
                sh ('terraform init');
            }
        }
        
        stage('terraform fmt') {
            steps {
                sh ('terraform fmt');
            }
        }
        
        stage('terraform validate') {
            steps {script{
            sh '''
                c=$(echo $/)
                echo $c
                if [ $c == 0 ]
                then
                  echo "the configuration file is valid"
                else
                  echo "your configuration file is not valid"
                fi    ''';
            }
        }}
        
        stage('terraform plan') {
            steps {
                sh ('terraform plan');
            }
        }
        
        stage('terraform destroy') {
            steps {
                sh 'terraform destroy --auto-approve'
            }
        }    
    }
}
