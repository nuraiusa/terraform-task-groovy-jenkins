# terraform-task-groovy-jenkins

node{
    stage("Pull Repo"){
        git branch: 'solution', url: 'https://github.com/nuraiusa/terraform-task-groovy-jenkins.git'
    }
    dir('sandbox') {
        withCredentials([usernamePassword(credentialsId: 'aws_jenkins_key', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
            stage("Terraform Init"){
            sh """
            terraform init
            """
        }
        stage("Terraform Apply"){
            sh """
            terraform apply -auto-approve
            """
        }
        }
}
}
