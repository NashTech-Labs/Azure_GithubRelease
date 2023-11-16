# Azure_GithubRelease
Use this task to create, edit, or delete a GitHub release. The following YAML creates a GitHub release every time the task runs. The build number is used as the tag version for the release..

## Pipeline Requirements

The dotNet Module pipeline requires the following parameters to be defined:

Parameters:

| Name  | Displayname | type | Default | Values | Opional/Required | Comments |
| ------------- | ------------- | :-------------: | :-------------: | :-------------: | :-------------: | ------------- |
| gitHubConnection | GitHub connection (OAuth or PAT) | String |  |  | Required | Specifies the name of the GitHub service connection to use to connect to the GitHub repository. The connection must be based on a GitHub user's OAuth or a GitHub personal access token |
| repositoryName | Repository | String | '$(Build.Repository.Name)' |  | Required | Specifies the name of the GitHub repository where you will create, edit, or delete the GitHub release |
| action | Action | String | 'create' | create, edit, delete | Required | Specifies the type of release operation to perform. This task can create, edit, or delete a GitHub release |
| target | Target | String | '$(Build.SourceVersion)' |  | Required | Specifies the commit SHA you want to use to create the GitHub release |
| tagSource | Tag source | String | gitTag | gitTag, userSpecifiedTag | Required | Required when action = create. Allowed values: gitTag (Git tag), userSpecifiedTag (User specified tag). Default value: gitTag. Specifies the tag you want to use for release creation. The gitTag option automatically uses the tag that is associated with the Git commit. Use the userSpecifiedTag option to manually provide a tag |
| tag | Tag | String | |  | Optional | Required when action = edit || action = delete || tagSource = userSpecifiedTag. Specifies the tag you want to use when you create, edit, or delete a release. You can also use a variable, like $(myTagName), in this field |

-----------------------------------------------------------------------------------------

These parameters provide multiple use case options for the dotnet templates pipeline, enable/disable flags for the utilization of different templates as per the requirements.


## Use Cases

You can directly call a particular template as per the requirement. for example: 

  ```yaml
  # azure-pipeline.yml
  resources:
  repositories:
    - repository: Template
      type: github
      name: your_username/Azure_GithubRelease
      ref: <respective branch name>
      endpoint: 'githubServiceConnectioNname'

  steps:
  # passing the parameters
  - template: GitHubRelease.yaml
    parameters:
      gitHubConnection: '${{ parameters.gitHubConnection }}'  
      repositoryName: '${{ parameters.repositoryName }}' 
      action: '${{ parameters.action }}' 
      target: '${{ parameters.target }}' 
      tagSource: '${{ parameters.tagSource }}'
      tag: '${{ parameters.tag }}'                  

  ```
Make sure to adjust the repository name, branch name, and parameter values according to your project's requirements.
