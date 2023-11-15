# DOESAQ3.yml

trigger:
  branches:
    include:
      - main
      - development

pool:
  vmImage: 'ubuntu-latest'

steps:
- script: echo 'Starting the build process...'
  displayName: 'Initialize Build'

- task: UseNode@1
  inputs:
    versionSpec: '14.x'
    displayName: 'Install Node.js'

- script: npm install
  displayName: 'Install Dependencies'

- script: npm run build
  displayName: 'Build Application'

- task: PublishBuildArtifacts@1
  inputs:
    pathtoPublish: 'dist'
    artifactName: 'myApp'

- script: echo 'Build process completed successfully.'
  displayName: 'Finalize Build'
