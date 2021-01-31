def remote = [:]
remote.name = "kub3"
remote.host = "192.168.61.52"
remote.allowAnyHosts = true

node {
    withCredentials([usernamePassword(credentialsId: 'kub3', passwordVariable: 'password', usernameVariable: 'userName')]) {
        remote.user = userName
        remote.password = password

        stage("SSH Steps Rocks!") {
            checkout scm
            sshPut remote: remote, from: 'docker-compose.yaml', into: '/root/'
            sshCommand remote: remote, command:  '''docker stack deploy -c docker-compose.yaml web'''
            sshCommand remote: remote, command: 'docker service ls'

            //sshScript remote: remote, script: 'test.sh'
           //sshPut remote: remote, from: 'test.sh', into: '/home/tanabat/'
           // sshGet remote: remote, from: 'test.sh', into: 'test_new.sh', override: true
           // sshRemove remote: remote, path: 'test.sh'
        }
        stage("TEST Web") {
            echo "do nothing"
            
        }
    }
}
