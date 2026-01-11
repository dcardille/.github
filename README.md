Reusable GitHub Actions Workflows
This repository contains reusable GitHub Actions workflows for my .NET projects.

Available Workflows
dotnet-release.yml	# Main reusable workflow
	Builds and releases .NET projects with automatic versioning via MinVer.

dotnet-build.yml        # Optional: just build, no release
	Future

dotnet-test.yml         # Optional: run tests
	Future

Features:

Builds single-file executables
Supports multiple runtimes (win-x64, linux-x64, etc.)
Automatic versioning from Git tags
Creates GitHub releases with downloadable artifacts
Framework-dependent or self-contained builds
Usage in your project:

yaml
# .github/workflows/release.yml
name: Release

on:
  push:
    tags:
      - '*.*.*'

jobs:
  release-windows:
    uses: yourusername/.github/.github/workflows/dotnet-release.yml@main
    with:
      project-path: 'src/MyApp/MyApp.csproj'
      runtime: 'win-x64'
      self-contained: false
Parameters:

Parameter	Description	Default	Required
project-path	Path to .csproj file	**/*.csproj	No
dotnet-version	.NET SDK version	10.0.x	No
runtime	Target runtime (win-x64, linux-x64, etc.)	win-x64	No
self-contained	Build as self-contained	false	No
create-release	Create GitHub release	true	No
Example: Multi-platform release

yaml
jobs:
  release-windows:
    uses: yourusername/.github/.github/workflows/dotnet-release.yml@main
    with:
      runtime: 'win-x64'
  
  release-linux:
    uses: yourusername/.github/.github/workflows/dotnet-release.yml@main
    with:
      runtime: 'linux-x64'
Requirements
Your .NET projects should:

Use MinVer for versioning (add MinVer NuGet package)
Use semantic version tags (e.g., 1.2.0, 2.0.0)
Have a .csproj file
Versioning Workflow
Make changes and commit
Create a tag: git tag 1.2.0
Push tag: git push origin 1.2.0
GitHub Actions automatically builds and creates release
License
MIT

