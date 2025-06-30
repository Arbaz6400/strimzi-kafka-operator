pipeline {
    agent any

    environment {
        MAVEN_SETTINGS_DIR = "${HOME}/.m2"
        MAVEN_SETTINGS_FILE = "${HOME}/.m2/settings.xml"
    }

    stages {
        stage('Prepare Maven Settings') {
            steps {
                script {
                    sh '''
                        mkdir -p $MAVEN_SETTINGS_DIR

                        cat > $MAVEN_SETTINGS_FILE <<EOF
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 
                              https://maven.apache.org/xsd/settings-1.0.0.xsd">
    <mirrors>
        <mirror>
            <id>central</id>
            <mirrorOf>central</mirrorOf>
            <url>https://repo.maven.apache.org/maven2</url>
        </mirror>
    </mirrors>
</settings>
EOF
                    '''
                }
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean install -DskipTests -U'
            }
        }
    }
}
