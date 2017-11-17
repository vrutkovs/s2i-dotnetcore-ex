node {
  stage("Build") {
      openshiftBuild buildConfig: "s2i-dotnetcore-ex", showBuildLogs: "true"
  }

  stage("Deploy to dev") {
      openshiftDeploy deploymentConfig: "s2i-dotnetcore-ex"
  }

  stage("Smoketest") {
      sh "curl -kLvs http://s2i-dotnetcore-ex:8080 | grep OPENSOURCE"
  }

  stage("Deploy to tested") {
      openshiftTag srcStream: "s2i-dotnetcore-ex", srcTag: 'latest', destinationStream: "s2i-dotnetcore-ex", destinationTag: "smoketested"
      openshiftDeploy deploymentConfig: "dotnet-smoketested"
  }
}
