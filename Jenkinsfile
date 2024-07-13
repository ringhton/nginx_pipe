pipeline {
    agent any 
    stages {
        stage('Cloning') { 
            steps {
                sh "sudo rm -rf *"               
                sh "git clone git@gitlab.rebrainme.com:devops_users_repos/5483/nginx_pipe.git"
     //           sh "cd nginx_pipe/"
            }
        }
        stage('Deploy') { 
            steps {               
                sh "sudo cp -r nginx_pipe/v0.1/ /var/www/"
                sh '''#!/bin/bash
                if [[ -L '/var/www/current' ]]; then sudo ln -sfT /var/www/v0.1/ /var/www/current; fi'''
                sh "sudo cp nginx_pipe/static_site /etc/nginx/sites-available/"
                sh '''#!/bin/bash
                if [[ -L '/etc/nginx/sites-enabled/static_site' ]]; then sudo ln -sfT /etc/nginx/sites-available/static_site /etc/nginx/sites-enabled/static_site; fi'''
                sh "sudo service nginx reload"
            }
        }
    }
}



