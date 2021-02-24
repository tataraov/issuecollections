node {
    def server
    buildInfo = Artifactory.newBuildInfo()
    buildInfo.name = 'super-frog'
    buildInfo.number = 'v:123'    
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
