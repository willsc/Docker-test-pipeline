podTemplate(
    name: 'test-pod',
    label: 'test-pod',
    containers: [
        containerTemplate(name: 'golang', image: 'golang:1.9.4-alpine3.7'),
        containerTemplate(name: 'gcloud', image:'gcr.io/cloud-builders/gcloud'),
    ],
    {
        //node = the pod label
        node('test-pod'){
            //container = the container label
            stage('Build'){
                container('golang'){
                    // This is where we build our code.
                }
            }
            stage('Build Docker Image'){
                container(‘gcloud’){
                    //This is where we build and push our Docker image.
                }
            }
        }
    })