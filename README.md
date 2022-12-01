# dotnet-sonar-scanner

Custom GitHub Action for running SonarScanner for .NET

## Minimal Configuration

```yaml
 -  name: Setup .Net
    uses: actions/setup-dotnet@v2
    with:
        dotnet-version: 6.0.403
        source-url: https://nuget.pkg.github.com/my-organization/index.json
    env:
        NUGET_AUTH_TOKEN: ${{ secrets.PACKAGES_TOKEN }}

 -  name: Run Sonar Scan
    uses: RightNowMinistries/dotnet-sonar-scanner@v1
    with: 
        dotnet-test-project: MyService.Tests.Unit
        sonar-login: ${{ secrets.SONAR_LOGIN }}
        sonar-project-key: my-sonar-project-key
        sonar-organization: "my-organization"
        sonar-code-coverage-exclusions: "MyService.Tests.Unit/**,**/Startup.cs"
```

## Full Configuration

```yaml
 -  name: Setup .Net
    uses: actions/setup-dotnet@v2
    with:
        dotnet-version: 6.0.403
        source-url: https://nuget.pkg.github.com/my-organization/index.json
    env:
        NUGET_AUTH_TOKEN: ${{ secrets.PACKAGES_TOKEN }}

 -  name: Run Sonar Scan
    uses: RightNowMinistries/dotnet-sonar-scanner@v1
    with: 
        dotnet-test-project: MyService.Tests.Unit
        sonar-login: ${{ secrets.SONAR_LOGIN }}
        sonar-project-key: my-sonar-project-key
        sonar-organization: "my-organization"
        sonar-url: "https://sonarcloud.io"
        sonar-exclusions: "**/Startup.cs"
        sonar-code-coverage-exclusions: "MyService.Tests.Unit/**"
        sonar-duplication-exclusions: "**/**Test.cs"
```

## Pre-requisites

This action requires that the .Net SDK is installed as needed to build and execute tests in the .Net project.

## Properties

### `dotnet-test-project`

*Optional*

Specify a test project name. If provided, only tests within this project will be executed. If left empty, all tests will be executed.

## `sonar-login`

*Required*

Credentials used to authenticate with SonarCloud.

## `sonar-project-key`

*Required*

SonarCloud project key used to analyze against and update reports.

## `sonar-organization`

*Required*

SonarCloud Organization Account key.

## `sonar-url`

*Optional*

URL to SonarQube instance. Customize if using a self-hosted instance of SonarQube. Defaults to SonarCloud URL (https://sonarcloud.io)

## `sonar-exclusions`

*Optional*

Comma separated list of file references excluded from Static Analysis.

## `sonar-code-coverage-exclusions`

*Optional*

Comma separated list of file references excluded from Code Coverage Analysis.

## `sonar-duplication-exclusions`

*Optional*

Comma separated list of file references excluded from Code Duplication Analysis.

## Versioning

This action follows similar patterns to versioning as other GitHub actions.

### Non-Breaking Changes

When a non-breaking change is published, we will increment the minor version for the action. Example: `1.1` -> `1.2`

### Breaking Changes

Whenver a change is made that alters the contract for require parameters, changes default values or changes major versions for the `dotnet-sonarscanner` tool that is used, the major version should be incremented. Example: `1.1` -> `2.0`.

### Tags

When introducing new versions, there should always be a `vX` and a `vX.Y` tag to pin the version. The `vX` tag should always reference the latest `vX.Y` tag where those major version matches. 

For example, if we introduce a version `2.2`, we should end up with a set of tags like:

| Tag | Commit Hash |
| --- | ----------- |
| v2.1 | #XYZ |
| v2.0 | #WXY |
| v2 | #XYZ |
| v1.1 | #ABC |
| v1.0 | #CBA |
| v1 | #ABC |

#### Create New Major Version Tag

```bash
git tag -a v1
git tag -a v1.0
git push origin --tags
```

#### Create New Minor Version Tag

```bash
git tag -af v1
git tag -a v1.1
git push origin -f --tags
```