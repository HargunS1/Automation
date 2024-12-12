pipeline {
    agent any
    environment {
        EC2_DEMO_HOST = 'ubuntu@50.112.122.55'
        AWS_KEY = credentials('aws-ec2-key1') // Jenkins credential for SSH
    }

    stages {
        stage('Run Monitoring Tools') {
            steps {
                script {
                    sshagent(['aws-ec2-key1']) {
                        sh """
                        ssh -o StrictHostKeyChecking=no $EC2_DEMO_HOST '
                        docker run -d --name=prometheus -p 9090:9090 -v /opt/prometheus/prometheus.yml:/etc/prometheus/prometheus.yml prom/prometheus &&
                        docker run -d --name=grafana -p 3000:3000 grafana/grafana
                        '
                        """
                    }
                }
            }
        }
    }
}
