Repro for issue https://github.com/NuGet/Home/issues/13453
=====

Repro steps:
0. Install the .NET SDK versions 8.0.205 and 8.0.300.
1. `cd src`
2. `dotnet restore`

    Success
3. change `src/global.json` SDK version to 8.0.300.
4. `dotnet restore` again

    Failure to resolve package version from `src/Directory.Packages.props`

Reason for failure:

The property `ManagePackageVersionsCentrally` specified in `/Directory.Build.props` is explicitly set to `false`, but is overridden in `/src/Directory.Packages.props`.  In the 205 SDK, that property override is accepted, but in 300 it is not.

Possible fix: Set the `ManagePackageVersionsCentrally` property in `/src`, either in the `.csproj` or in a new `Directory.Build.props` file.
