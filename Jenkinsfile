node {

    def server = Artifactory.server 'auditsg'
    // def server = Artifactory.newServer url: 'https://auditsg.jfrog.io/artifactory', username: 'fimtestxyz@gmail.com', password: 'M0t0r0la@@'
    def buildInfo = Artifactory.newBuildInfo()
    buildInfo.name = 'desktop-tutorial-build'
    println('-------- Pre-setup --------')
    println(buildInfo)
    println(buildInfo.name)
    println(buildInfo.number)
    
    
    
    def formatToLowerCaseClosure = { name ->
    return name.toUpperCase()
}
    
    stage('Checkout from Github') {
        git branch: 'main', url: 'https://github.com/fimtestuvw/desktop-tutorial'
    }
    
    stage('Setup Artifactory server') {
       
        echo 'setup artifactory server'
        
    }
    // stage('Download Spec'){
    //     println(server)
    //     def downloadSpec = """{
    //      "files": [
    //       {
    //           "pattern": "uob_auditor_repo/*.*",
    //           "target": "uob_auditor_repo/"
    //         }
    //      ]
    //     }"""
    //     server.download spec: downloadSpec, failNoOp : true
    // }
    stage('Upload Spec'){
        def uploadSpec = """{
          "files": [
            {
              "pattern": "*",
              "flat" : false,
              "excludePatterns" : [".git/*"],
              "target": "uob_auditor_repo/desktop-tutorial/"
            }
         ]
        }"""
        

    
    server.upload spec: uploadSpec, failNoOp : false, buildInfo: buildInfo
    println('-------- AFter upload, Buildinfo --------')
    println(buildInfo)
    println(buildInfo.name)
    println(buildInfo.number)
    
    def setPropsSpec = """{
         "files": [
          {
               "pattern": "uob_auditor_repo/desktop-tutorial/*.*"
            }
         ]
        }"""
     
    server.setProps spec: setPropsSpec, props: "p1=v11;p2=v22;p3=v33"
    }
    
    // def newbuildInfo = Artifactory.newBuildInfo()

    
    stage('PUblish BuildInfo'){
        server.publishBuildInfo buildInfo
        println('----------After Publish-------------------')
        println(buildInfo)
        println(buildInfo.name)
        println(buildInfo.number)

    }
    
    stage('Promote Buid'){
        
        def promotionConfig = [
            // Mandatory parameters
            'targetRepo'         : 'uob_auditor_repo_staging',
         
            // Optional parameters
         
            // The build name and build number to promote. If not specified, the Jenkins job's build name and build number are used
            'buildName'          : buildInfo.name,
            'buildNumber'        : buildInfo.number,
            // Comment and Status to be displayed in the Build History tab in Artifactory
            'comment'            : 'this is a promoted by wengkoon',
            'status'             : 'Released-by-inakamono',
            // Specifies the source repository for build artifacts.
            'sourceRepo'         : 'uob_auditor_repo',
            // Indicates whether to promote the build dependencies, in addition to the artifacts. False by default
            'includeDependencies': true,
            // Indicates whether to copy the files. Move is the default
            'copy'               : true,
            // Indicates whether to fail the promotion process in case of failing to move or copy one of the files. False by default.
            'failFast'           : true
        ]
        
        def promo_info = server.promote promotionConfig
        println(promo_info)
        // def x = formatToLowerCaseClosure('Done. Yahoo')
        println(formatToLowerCaseClosure('Done!!! Yahoo .....inakamono'))
        // println(x)
    }
    
    // def show_info = {
    //     println(localPath)
    //     println(remotePath)
    //     println(md5)
    //     println(sha1)
    // }
    
    // stage('Show Info'){
    //     if (buildInfo.getDependencies().size() > 0) {
    //         def localPath = buildInfo.getDependencies()[0].getLocalPath()
    //         def remotePath = buildInfo.getDependencies()[0].getRemotePath()
    //         def md5 = buildInfo.getDependencies()[0].getMd5()
    //         def sha1 = buildInfo.getDependencies()[0].getSha1()
    //         show_info()
    //     }
         
    //     if (buildInfo.getArtifacts().size() > 0) {
    //         def localPath = buildInfo.getArtifacts()[0].getLocalPath()
    //         def remotePath = buildInfo.getArtifacts()[0].getRemotePath()
    //         def md5 = buildInfo.getArtifacts()[0].getMd5()
    //         def sha1 = buildInfo.getArtifacts()[0].getSha1()
    //         show_info
    //     }
    // }
}



