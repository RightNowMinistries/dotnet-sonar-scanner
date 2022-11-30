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
