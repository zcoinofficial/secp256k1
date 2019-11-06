pipeline {
    agent {
        docker { image 'zcoinofficial/zcoin-builder:latest' }
    }
    stages {
        stage('Build') {
            steps {
                sh 'git clean -d -f -f -q -x'
                sh './autogen.sh'
                sh './configure'
                sh 'make dist'
                sh 'mkdir -p dist'
                sh 'tar -C dist --strip-components=1 -xzf libsecp256k1-*.tar.gz'
                dir('dist') {
                    sh './configure'
                    sh 'make -j6'
                }
            }
        }
        stage('Test') {
            steps {
                dir('dist') {
                    sh 'make check'
                }
            }
        }
    }
}
