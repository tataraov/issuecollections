node {
    def server
    buildInfo = Artifactory.newBuildInfo()
    stage("Initialization") {
        steps {
            // use name of the patchset as the build name
            buildName "build#2"
            buildDescription "Executed @ ${NODE_NAME}"
            }
        }
    stage ('Build') {
        git url: 'https://github.com/jfrog/jenkins-artifactory-plugin.git'
        server = Artifactory.server 'Artifactory'

        issuesCollectionConfig = """{
            "version": 1,
            "issues": {
                "trackerName": "JIRA",
                "regexp": "(.+-[0-9]+)\\s-\\s(.+)",
                "keyGroupIndex": 1,
                "summaryGroupIndex": 2,
                "trackerUrl": "http://my-jira.com/issues",
                "aggregate": "true",
                "aggregationStatus": "RELEASED"
            }
        }"""

        buildInfo.issues.collect(server, issuesCollectionConfig)

        server.publishBuildInfo buildInfo
    }
}
