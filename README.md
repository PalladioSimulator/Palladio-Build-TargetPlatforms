# Palladio-Build-TargetPlatforms

This repository provides a collection of shared target platform definitions for Tycho-based builds of Palladio. Each target platform bundles a specific Eclipse Modeling release alongside Palladio-specific branding and license features, ensuring a consistent development environment across projects.

## Available Target Platforms

Each of the following target platforms corresponds to an Eclipse Modeling release. The numeric suffix (e.g., `2023-09`)
in the target platform name (`palladio-YYYY-MM`) indicates the the year and month of the respective Eclipse Simultaneous
Release version that the target platform is based on.

| Target Platform Name | Eclipse Modeling Release |
| -------------------- | ------------------------ |
| `palladio-2020-12`   | 2020‑12                  |
| `palladio-2021-12`   | 2021‑12                  |
| `palladio-2022-12`   | 2022‑12                  |
| `palladio-2023-03`   | 2023‑03                  |
| `palladio-2023-06`   | 2023‑06                  |
| `palladio-2023-09`   | 2023‑09                  |

You can find the `.target` definitions in the [`targetPlatforms/`](targetPlatforms/) directory.

## Usage

To use one of the target platforms in your project, add a `<location>` element with the type `"Target"` and the URI pointing to the Maven‑hosted artifact of the desired target platform to your own `.target` file:

```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<?pde version="3.8"?><target name="org.palladiosimulator.example Target Platform">
    <locations>
        <!-- Add this location element -->
        <location type="Target" uri="mvn:org.palladiosimulator:palladio-target-platforms:{version}:target:palladio-{YYYY-MM}"/>

        <!-- You may add other locations here -->
    </locations>
</target>
```

Replace `{version}` with the latest released version of this project (e.g., `0.1.0`) and `{YYYY-MM}` with the year and month of the desired target platform.

**Example** (using version `0.1.0` and the `palladio-2023-09` target platform):

```xml
<location type="Target" uri="mvn:org.palladiosimulator:palladio-target-platforms:0.1.0:target:palladio-2023-09"/>
```

For a complete implementation example showing the usage of nested `.target` references, see Tycho's [target reference integration test](https://github.com/eclipse-tycho/tycho/tree/main/tycho-its/projects/target.references/target.refs).

> [!NOTE]
> To use nested `.target` references within the Eclipse IDE (e.g., via PDE's Target Editor), make sure you are using Eclipse IDE 2022‑03 (version 4.23) or newer. In addition, referencing a Maven-hosted target platform using the `mvn:` URI syntax requires m2e (m2eclipse) with PDE (Plug-in Development Environment) integration. See [Eclipse 4.23 New & Noteworthy – Reference an existing target inside another one](https://eclipse.dev/eclipse/news/4.23/pde.html#pde-editor-include) for details.
