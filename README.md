# Generate-Nupkg
Generate a Refit client interface and contracts from an OpenAPI specifications document using [Refitter](https://github.com/christianhelle/refitter).

## Inputs

### `openapi-file`
The path to the OpenAPI document (both JSON and YAML are supported). Defaults to "openapi.json" (i.e. a file in the current directory called openapi.json). Paths that do not start with `/` are assumed to be relative to the root of the repository.

### `openapi-url`
The URL to load the OpenAPI document from. If set, `openapi-file` will be ignored.

### `namespace`
The default namespace used for the generated types (default: `GeneratedCode`)

### `use-api-response`
Return `Task<IApiResponse<T>>` instead of `Task<T>`

### `cancellation-tokens`
Use cancellation tokens

### `multiple-interfaces`
Generate a Refit interface for each endpoint. May be one of `ByEndpoint`, `ByTag`

### `command-args`
Additional arguments to pass through to the [Refitter](https://github.com/christianhelle/refitter) CLI tool.

### `publish-artifacts`
Publish the generated nuget package as a build artifact

### `output-filename`
No outputs are returned. The generated client is placed in the current directory and using the `output-filename` (Default: **`Output.cs`**) value. The output file contains both the Refit interface and the contract types used by the API

### `version`
The version number used for the NuGet package (default: `1.0.${{ github.run_number }}`)

### `target-framework`
The target framework used in the generated Client SDK (default: `net6.0`)

### `package-id`
The value used as `<PackageId>` for package the generated code into a NuGet package

### `title`
The value used as `<Title>` for package the generated code into a NuGet package

### `root-namespace`
The value used as `<RootNamespace>` for package the generated code into - a NuGet package

### `assembly`
The value used as `<AssemblyName>` for package the generated code into a - NuGet package

### `authors`
The value used as `<Authors>` for package the generated code into a NuGet - package

### `company`
The value used as `<Company>` for package the generated code into a NuGet - package

### `product`
The value used as `<Product>` for package the generated code into a NuGet - package

### `description`
The value used as `<Description>` for package the generated code into a - NuGet package

### `license`
The value used as `<PackageLicenseExpression>` for package the generated code - into a NuGet package

### `project-url`
The value used as `<PackageProjectUrl>` and `<RepositoryUrl>` for package - the generated code into a NuGet package

### `repository-type`
The value used as `<RepositoryType>` for package the generated code into a NuGet package


# Examples

### Using a URL and producing a Client SDK NuGet package

```yaml
jobs:
  smoke-test-url-with-client-sdk:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      # Use the action to generate a Refit client interface
      # This produces a NuGet package as a build artifact
      - uses: refitter/generate-nupkg@v1
        name: Generate Refit Client SDK
        with:
          openapi-url: https://petstore3.swagger.io/api/v3/openapi.json
          namespace: ChristianHelle.Examples.Petstore.v3
          client-sdk: true
          version: 3.0.${{ github.run_number }}
          package-id: ChristianHelle.Examples.Petstore.v3
          title: ChristianHelle.Examples.Petstore.v3
          root-namespace: ChristianHelle.Examples.Petstore.v3
          assembly: ChristianHelle.Examples.Petstore.v3
          product: ChristianHelle.Examples.Petstore.v3
          authors: Christian Resma Helle
          company: Christian Resma Helle
          description: Example generated code using Refitter and the Swagger Petstore v3 example OpenAPI specifications
          project-url: https://github.com/christianhelle/refitter
```
