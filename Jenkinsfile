pipeline {
    agent any

    stages {
        stage('Preparing gradlew') {
            steps {
                sh 'chmod +x gradlew'
            }
        }
        stage('test') {
            steps {
                sh './gradlew test'
            }
        }
        stage('build') {
            steps {
                sh './gradlew build'
            }
        }
        stage('Release') {
            steps {
                sh '''
                token="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"
                # Get the last tag name
                tag=$(git describe --tags)
                # Get the full message associated with this tag
                message="$(git for-each-ref refs/tags/$tag --format='%(contents)')"

                # Get the title and the description as separated variables
                name=$(echo "$message" | head -n1)
                description=$(echo "$message" | tail -n +3)
                description=$(echo "$description" | sed -z 's/\n/\\n/g') # Escape line breaks to prevent json parsing problems

                # Create a release
                release=$(curl -XPOST -H "Authorization:token $token" --data "{\"tag_name\": \"$tag\", \"target_commitish\": \"main\", \"name\": \"$name\", \"body\": \"$description\", \"draft\": false, \"prerelease\": false}" https://api.github.com/repos/YoussF/caesar-cipher/releases)

                # Extract the id of the release from the creation response
                id=$(echo "$release" | sed -n -e 's/"id":\ \([0-9]\+\),/\1/p' | head -n 1 | sed 's/[[:blank:]]//g')

                # Upload the artifact
                curl -XPOST -H "Authorization:token $token" -H "Content-Type:application/octet-stream" --data-binary @build/libs/caesar-cipher-$tag.jar https://uploads.github.com/repos/YoussF/caesar-cipher/releases/$id/assets?name=caesar-cipher-$tag.jar
                '''

            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}