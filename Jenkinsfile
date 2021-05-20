node('jenkins-slave') {
    
     stage('test pipeline') {
        sh(script: """
            echo "hello"
           git clone https://github.com/ceptravi/dockerdemo.git
           cd ./docker-development-youtube-series/golang
           
           docker build . -t test
        """)
    }
}