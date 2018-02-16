import groovy.json.*

pipeline {
    agent { label "dynamic-jp" }
    stages {
        stage ("hoge") {
            steps {
                echo "Hello World"
                notify("SUCCESS")
            }
        }
    }
}

def notify(String result, String msg = "") {
    def color
    switch (result) {
        case "SUCCESS":
            color = '#00FF00';
            break;
        case "UNSTABLE":
            color = '#FFFF00';
            break;
        case "FAILURE":
            color = '#FF0000';
            break;
        default:
            color = '#888888';
    }
    def url = "https://outlook.office.com/webhook/794bf4b6-5a42-409a-a4db-42fccc75e52d@e0793d39-0939-496d-b129-198edd916feb/IncomingWebhook/1f04e79fa4c341dd8b5e4d9e110f191e/1391f8d1-bfb9-4524-9cf2-20ee8265003c"
    def str = "${msg}<br/>${result}: Job '${env.JOB_NAME} [#${env.BUILD_NUMBER}]' ${env.BRANCH_NAME} <br/><${env.BUILD_URL}>";
    office365ConnectorSend status: result, color: color, message: str, webhookUrl: url
}