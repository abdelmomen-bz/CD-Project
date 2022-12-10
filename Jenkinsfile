pipeline
{
    agent any
     stages {
      
        stage(' GIT ') {
            steps {
                echo 'Pulliing ...';
                git branch: 'master', url: 'https://github.com/abdelmomen-bz/CD-Project.git'          
            }
     
        }
        stage(' install node modules ') {
            steps {
            sh ' npm install' 
            
            }
        }

/*
        stage(' BUILD ') {
            steps {
            sh ' npm run build --prod'
            }
        } */

        stage(' BUILD ') {
            steps {
                script {
                    sh ' ansible-playbook ansible/build.yml -i ansible/inventory/host.yml '
                 }
            }
        }

        stage(' DOCKER ') {
            steps {
                script {
                    sh ' ansible-playbook ansible/docker.yml -i ansible/inventory/host.yml '
                 }
            }
        }


        stage(' DOCKER REGISTRY') {
            steps {
                withDockerRegistry([credentialsId: "docker-hubb", url: ""]) {
                script {
                    sh ' ansible-playbook ansible/docker-registry.yml -i ansible/inventory/host.yml '
                 }
                 }
            }
        }