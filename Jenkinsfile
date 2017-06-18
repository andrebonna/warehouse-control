// node('docker-slave') {
//     checkout scm
//     echo 'Building..'
//
//     sh "npm install"
//     sh "npm start"
//     sh "npm test"
//
//
// }

def hostIp(container) {
  def ip = sh script: "docker inspect --format='{{.NetworkSettings.IPAddress}}' ${container.id}", returnStdout: true
  return ip.trim()
  // return readFile('hostIp').trim()
}

docker.image('mongo').withRun('-p 27025:27017') {c ->

    def mongo = hostIp(c)
    node('docker') {
        checkout scm
        echo 'Building..'

        sh "npm install"
        sh "MONGO_DB=${mongo} MONGO_DB_PORT=27025 npm start"
        sh "npm test"

    }
    //echo "http://${readFile('hostIp').trim()}:27025/"
}
