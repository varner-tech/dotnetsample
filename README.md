# .NET Home

This repository is a starting point to learn about and engage in .NET and .NET open source projects.

This repository is not an official .NET Framework support location, however, we will respond to issues filed here as best we can. Please file .NET Core product issues at [dotnet/core](https://github.com/dotnet/core/issues) and ASP.NET Core product issues at [aspnet/home](https://github.com/aspnet/home/issues).

You can try out an early access release of the .NET Framework at the [.NET Framework Early Access](https://github.com/microsoft/dotnet-framework-early-access) website.

---

## Snyk Security Testing Guide

This guide walks you through scanning this .NET repository for security vulnerabilities using Snyk. Follow these steps to perform Software Composition Analysis (SCA) and Static Application Security Testing (SAST), then monitor results in the Snyk dashboard.

### Prerequisites

Before you begin, ensure you have the following installed:

- **Git** - [Download Git](https://git-scm.com/downloads)
- **.NET SDK** - [Download .NET](https://dotnet.microsoft.com/download) (required for `dotnet restore`)
- **Snyk CLI** - Install via npm: `npm install -g snyk`
- **Snyk Account** - [Sign up for free](https://app.snyk.io/signup)

### Step 1: Clone the Repository

```bash
git clone https://github.com/varner-tech/dotnetsample.git
cd dotnetsample
```

### Step 2: Authenticate with Snyk

Log in to your Snyk account to enable dashboard monitoring:

```bash
snyk auth
```

This opens a browser window. Complete the authentication, then return to your terminal.

### Step 3: Restore .NET Dependencies

**This step is required before SCA scanning.** The `dotnet restore` command generates the `project.assets.json` file that Snyk needs to analyze NuGet dependencies.

```bash
dotnet restore src/bc-readme-gen/bcreadgen.csproj
```

> **Note:** If your project has a solution file (`.sln`) in the root directory, you can simply run `dotnet restore` without specifying a path.

### Step 4: Run SCA Scan (Software Composition Analysis)

Scan all projects for known vulnerabilities in open source dependencies:

```bash
snyk test --all-projects
```

This scans all .NET projects in the repository and displays vulnerabilities locally in your terminal.

### Step 5: Monitor in Snyk Dashboard (SCA)

Upload your SCA scan results to the Snyk dashboard for continuous monitoring:

```bash
snyk monitor --all-projects --project-name-prefix="sca/"
```

This creates a project named `sca/dotnetsample` in the Snyk dashboard.

### Step 6: Run SAST Scan (Snyk Code)

Scan your source code for security issues using static analysis:

```bash
snyk code test
```

### Step 7: Upload Code Scan to Dashboard

Upload your SAST results to the Snyk dashboard:

```bash
snyk code test --report --project-name="sast/dotnetsample"
```

This creates a project named `sast/dotnetsample` in the Snyk dashboard.

> **Note:** SCA and SAST scans appear as **separate targets** in the Snyk dashboard. This is by design—Snyk Open Source (SCA) and Snyk Code (SAST) are different products with different scan types. Use the `sca/` and `sast/` prefixes to easily identify which scan type each project represents.

---

### Command Summary

| Task | Command |
|------|---------|
| Clone repository | `git clone https://github.com/varner-tech/dotnetsample.git` |
| Authenticate with Snyk | `snyk auth` |
| Restore .NET dependencies | `dotnet restore src/bc-readme-gen/bcreadgen.csproj` |
| SCA scan (local) | `snyk test --all-projects` |
| SCA scan + dashboard | `snyk monitor --all-projects --project-name-prefix="sca/"` |
| SAST scan (local) | `snyk code test` |
| SAST scan + dashboard | `snyk code test --report --project-name="sast/dotnetsample"` |

---

### .NET-Specific Options

#### Scanning Solution Files

To scan a specific solution file:

```bash
snyk test --file=MySolution.sln --all-projects
```

#### Understanding Snyk Targets

SCA (Snyk Open Source) and SAST (Snyk Code) scans will appear as **separate targets** in the Snyk dashboard. This is expected behavior—they are different Snyk products with different scan types.

**Dashboard structure:**
- **Open Source target:** Contains `sca/projectname` (dependency vulnerabilities)
- **Snyk Code target:** Contains `sast/projectname` (code vulnerabilities)

Use clear naming prefixes to easily identify scan types:

**For SCA scans:**
```bash
snyk monitor --all-projects --project-name-prefix="sca/"
```

**For SAST scans:**
```bash
snyk code test --report --project-name="sast/projectname"
```

**Key flags:**
- `--project-name-prefix` - Adds prefix for SCA projects (used with `--all-projects`)
- `--project-name` - Sets exact name for SAST scans

---

### Troubleshooting

#### "Could not detect supported target files"

**Cause:** The `project.assets.json` file is missing.

**Solution:** Run `dotnet restore` before scanning:

```bash
dotnet restore src/bc-readme-gen/bcreadgen.csproj
snyk test --all-projects
```

#### Scanning a Fresh Clone

When scanning a repository you've just cloned, always restore dependencies first:

```bash
git clone https://github.com/varner-tech/dotnetsample.git
cd dotnetsample
dotnet restore src/bc-readme-gen/bcreadgen.csproj
snyk test --all-projects
```

#### Authentication Issues

If you receive authentication errors, re-authenticate:

```bash
snyk auth
```

#### Verbose Output for Debugging

Add `-d` for debug output to troubleshoot issues:

```bash
snyk test --all-projects -d
```

---

## In this repository

- [.NET Framework Release Notes](releases/README.md)
- [.NET Framework Documentation](Documentation/README.md)
- [.NET Open Source Developer Projects](dotnet-developer-projects.md)
- [.NET Open Source Consumer Projects](dotnet-consumer-projects.md)
- [Free Services & Tools for Open Source .NET Projects](dotnet-free-oss-services.md)

Please contribute to this repository via [pull requests](https://github.com/Microsoft/dotnet/pulls)

## Finding .NET Open Source Projects

Here are some excellent community-maintained lists of projects:

- [Awesome .NET!](https://github.com/quozd/awesome-dotnet)
- [ASP.NET Core Library and Framework Support](https://github.com/jpsingleton/ANCLAFS)

There are many projects that you can use and contribute to, some of which are listed below. Please do contribute to these projects!

### .NET Core

- [.NET Core (dotnet/core)](https://github.com/dotnet/core)
- [.NET Core docs (dotnet/docs)](https://github.com/dotnet/docs)
- [ASP.NET Core (dotnet/aspnetcore)](https://github.com/dotnet/aspnetcore)
- [ASP.NET Core docs (dotnet/AspNetCore.Docs)](https://github.com/dotnet/AspNetCore.Docs)
- [Roslyn Compiler Platform (dotnet/roslyn)](https://github.com/dotnet/roslyn)
- [EntityFramework (dotnet/efcore)](https://github.com/dotnet/efcore)
- [WPF (dotnet/wpf)](https://github.com/dotnet/wpf)
- [Windows Forms (dotnet/winforms)](https://github.com/dotnet/winforms)

### .NET Framework

- [.NET Framework docs (dotnet/docs)](https://github.com/dotnet/docs)
- [.NET Framework source code - read-only subset (microsoft/referencesource)](https://github.com/microsoft/referencesource)

### Xamarin

- [Xamarin iOS + macOS (xamarin-macios)](https://github.com/xamarin/xamarin-macios)
- [Xamarin Android (xamarin/xamarin-android)](https://github.com/xamarin/xamarin-android)
- [Xamarin Forms (xamarin/Xamarin.Forms)](https://github.com/xamarin/Xamarin.Forms)
- [Mono Project](https://github.com/mono/)

### Community

Here is a short list of projects to check out:

* [.NET for Apache Spark](https://github.com/dotnet/spark)
* [Orleans](https://github.com/dotnet/orleans)
* [Exceptionless](https://github.com/exceptionless/Exceptionless)
* [Glimpse](https://github.com/Glimpse/Glimpse)
* [JSON.NET](https://github.com/JamesNK/Newtonsoft.Json)
* [MonoGame](https://github.com/MonoGame/MonoGame)
* [MVVM Cross](https://github.com/MvvmCross/MvvmCross)
* [ReactiveUI](https://github.com/reactiveui/ReactiveUI)

There are additional templates available for `dotnet new`. For more information, see [Available templates for dotnet new](https://github.com/dotnet/templating/wiki/Available-templates-for-dotnet-new)

## .NET Foundation

Many .NET open source projects are part of the
[.NET Foundation](https://www.dotnetfoundation.org/projects). Microsoft has contributed many projects, including ASP.NET Core and
.NET Core. You may want to consider [joining the .NET Foundation](https://dotnetfoundation.org/community/).

Check out the [.NET Foundation Forums](https://forums.dotnetfoundation.org/) to see what others are talking about, or start a new discussion to ask a question or make a point. 

## License

This repository is licensed with the [MIT](LICENSE) license.
