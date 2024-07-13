pipeline { 
    agent any 
    stages {
        stage('Cloning') { 
            steps {
                sh "sudo rm -rf *"               
                sh "git clone git@gitlab.rebrainme.com:devops_users_repos/5483/nginx_pipe.git"
            }
        }
        stage('Deploy') { 
            steps {               
                sh "if [ -d /var/www/\$(git tag --points-at HEAD) ]; then sudo mkdir /var/www/\$(git tag --points-at HEAD); fi"
                sh "sudo cp -r nginx_pipe/index.html /var/www/\$(git tag --points-at HEAD)"
                sh "if [ -L /var/www/current ]; then sudo ln -sfT /var/www/\$(git tag --points-at HEAD) /var/www/current; fi"
                sh "sudo cp nginx_pipe/static_site /etc/nginx/sites-available/"
                sh "if [ -L /etc/nginx/sites-enabled/static_site ]; then sudo ln -sfT /etc/nginx/sites-available/static_site /etc/nginx/sites-enabled/static_site; fi"
                sh "sudo service nginx reload"
            }
        }
    }
}
