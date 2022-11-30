# dotnet-sonar-scanner
Custom GitHub Action for running SonarScanner for .NET

## Sample Configuration

```yaml
 -  name: Run Sonar Scan
    uses: RightNowMinistries/dotnet-sonar-scanner@v1
    with: 
        dotnet-version: 3.1.100
        dotnet-test-project: MyService.Tests.Unit
        nuget-source-url: https://nuget.pkg.github.com/my-organization/index.json
        nuget-auth-token: ${{ secrets.PACKAGES_TOKEN }}
        sonar-login: ${{ secrets.SONAR_LOGIN }}
        sonar-project-key: my-sonar-project-key
        sonar-organization: "my-organization"
        sonar-code-coverage-exclusions: "MyService.Tests.Unit/**,**/Startup.cs"
```

## Properties

### `dotnet-version`

**Required**

DotNet SDK version used to build and test the application.

### Example

```yaml
with:
    dotnet-version: 3.1.100
```

### `dotnet-test-project`

**Optional**

Specify a test project name. If provided, only tests within this project will be executed. If left empty, all tests will be executed.

### Example

```yaml
with:
    dotnet-test-project: "MyService.Tests.Unit"
```

### `nuget-source`

**Optional**

Allows you to provide a url for a custom/private Nuget feed. If a private feed is used, be sure to provide the [`nuget-auth-token`](#nuget-auth-token) property as well.

### Example

```yaml
with:
    nuget-source: https://nuget.pkg.github.com/my-organization/index.json
```

### `nuget-auth-token`

**Optional**

Allows you to provide a secure auth token to access nuget feed specified in [`nuget-source`](#nuget-source).

### Example

```yaml
with:
    nuget-source: https://nuget.pkg.github.com/my-organization/index.json
    nuget-auth-token: ${{ secrets.PACKAGES_TOKEN }}
```

## `sonar-login`

Credentials used to authenticate with SonarCloud.

### Example

```yaml
with:
    sonar-login: ${{ secrets.SONAR_LOGIN }}
```

## `sonar-project-key`

## `sonar-scanner-version`

## `sonar-organization`

## `sonar-url`

## `sonar-exclusions`

## `sonar-code-coverage-exclusions`

## `sonar-duplication-exclusions`
