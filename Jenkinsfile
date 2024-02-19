pipeline{
           agent any
           environment {
                      DOCKERHUB_CREDENTIALS=credentials('dockerhub')
           }
           stages {
                      stage('Build') {
                                    steps {
                                                sh 'docker build -t ahmedwahid/angular-demo-test:v1 .'
                                          }
                      }
                      stage('Login') {
                                    steps {
                                                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                                          }
                      }
                      stage('Push') {
                                    steps {
                                                sh 'docker push ahmedwahid/angular-demo-test:v1'
                                          }
                      }
                      stage('deploy') {
                                    steps {
                                                sh 'docker run -d -p 5200:5200 --name app-1 ahmedwahid/angular-demo-test:v1'
                                          }
                      }
           }
           post {
                      always {
                                                sh 'docker logout'
                             }
                }
}
