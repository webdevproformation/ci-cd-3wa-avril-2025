pipeline {
    agent any
    stages {
        stage('build') {
            agent {
                docker {
                    image 'node:20-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    echo 'jenkins va installer les dépendances du projet'
                    ls -al
                    npm ci 
                    echo 'Jenkins va créer le build'
                    npm run build
                    echo 'fin'
                    ls -al
                '''
            }
        }
        stage('test') {
            agent {
                docker {
                    image 'node:20-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    echo "lancement des tests"
                    test -f dist/index.html
                    npm run test 
                '''
            }
        }

        stage('push on dockergithub'){
            steps {
                sh '''
                    docker --version
                    # au préalable nous avons créé un dockerhub 
                    # généré depuis le profil un "Personal Access Token"
                    # ajouter dans notre dossier travail un fichier Dokerfile
                    # docker build -t malikh551/exo2_php
                    # docker login identifiant 
                    # docker push 
                '''
            }
        }

        stage('deployment'){
            steps {
                sh '''
                    echo "lancement de la phase de déploiement"
                    # au préalable nous avons créer l'EC2 et installé docker dedans
                    # docker pull malikh551/exo2_php
                    # docker run -d -p 80:80 malikh551/exo2_php 
                '''
            }
        }
    }
}