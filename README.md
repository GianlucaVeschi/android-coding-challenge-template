# androidkotlintemplate

![Build](https://github.com/GianlucaVeschi/android-kotlin-template/workflows/Pre%20Merge%20Checks/badge.svg)

This is your new Kotlin Android Project! Happy hacking!

## Template ToDo list 👣

- [x] Create a new template project.
- [ ] Choose a [LICENSE](https://github.com/GianlucaVeschi/android-kotlin-template/community/license/new?branch=main).
- [ ] Set your `ORG_GRADLE_PROJECT_NEXUS_USERNAME`, `ORG_GRADLE_PROJECT_NEXUS_PASSWORD`, `ORG_GRADLE_PROJECT_SIGNING_KEY` and `ORG_GRADLE_PROJECT_SIGNING_PWD` secrets in [Settings](https://github.com/GianlucaVeschi/android-kotlin-template/settings/secrets/actions).
- [ ] Code some cool apps and libraries 🚀.

## Features 🎨

- **100% Kotlin-only template**.
- Jetpack Compose setup ready to use. 
- Sample Espresso, Instrumentation & JUnit tests.
- 100% Gradle Kotlin DSL setup.
- CI Setup with GitHub Actions.
- Publish to **Maven Central** with Github Actions.
- Dependency versions managed via `buildSrc`.
- Kotlin Static Analysis via `detekt` and `ktlint`.
- Issues Template (bug report + feature request).
- Pull Request Template.

## Gradle Setup 🐘

This template is using [**Gradle Kotlin DSL**](https://docs.gradle.org/current/userguide/kotlin_dsl.html) as well as the [Plugin DSL](https://docs.gradle.org/current/userguide/plugins.html#sec:plugins_block) to setup the build.

Dependencies are centralized inside the Gradle Version Catalog in the [libs.versions.toml](gradle/libs.versions.toml) file in the `gradle` folder.

## Static Analysis 🔍

This template is using [**detekt**](https://github.com/detekt/detekt) to analyze the source code, with the configuration that is stored in the [detekt.yml](config/detekt/detekt.yml) file (the file has been generated with the `detektGenerateConfig` task). It also uses the **detekt-formatting** plugin which includes the ktlint rules (see https://detekt.dev/docs/rules/formatting/).

## CI ⚙️

This template is using [**GitHub Actions**](https://github.com/cortinico/kotlin-android-template/actions) as CI. You don't need to setup any external service and you should have a running CI once you start using this template.

There are currently the following workflows available:
- [Validate Gradle Wrapper](.github/workflows/gradle-wrapper-validation.yml) - Will check that the gradle wrapper has a valid checksum
- [Pre Merge Checks](.github/workflows/pre-merge.yaml) - Will run the `build`, `check` and `publishToMavenLocal` tasks.
- [Publish Snapshot](.github/workflows/publish-snapshot.yaml) - Will publish a `-SNAPSHOT` of the libraries to Sonatype.
- [Publish Release](.github/workflows/publish-release.yaml) - Will publish a new release version of the libraries to Maven Central on tag pushes.

## Publishing 🚀

The template is setup to be **ready to publish** a library/artifact on a Maven Repository.

For every module you want to publish you simply have to add the `publish` plugin:

```
plugins {
    publish
}
```

### To Maven Central

In order to use this template to publish on Maven Central, you need to configure some secrets on your repository:

| Secret name | Value |
| --- | --- | 
| `ORG_GRADLE_PROJECT_NEXUS_USERNAME` | The username you use to access Sonatype's services (such as [Nexus](https://oss.sonatype.org/) and [Jira](https://issues.sonatype.org/)) |
| `ORG_GRADLE_PROJECT_NEXUS_PASSWORD` | The password you use to access Sonatype's services (such as [Nexus](https://oss.sonatype.org/) and [Jira](https://issues.sonatype.org/)) |
| `ORG_GRADLE_PROJECT_SIGNING_KEY` | The GPG Private key to sign your artifacts. You can obtain it with `gpg --armor --export-secret-keys <your@email.here>` or you can create one key online on [pgpkeygen.com](https://pgpkeygen.com). The key starts with a `-----BEGIN PGP PRIVATE KEY BLOCK-----`. |
| `ORG_GRADLE_PROJECT_SIGNING_PWD` | The passphrase to unlock your private key (you picked it when creating the key). |

The template already sets up [Dokka](https://kotlin.github.io/dokka/) for project documentation and attaches `-sources.jar` to your publications,
via the new AGP publishing DSL.

Once set up, the following workflows will take care of publishing:

- [Publish Snapshot](.github/workflows/publish-snapshot.yaml) - To publish `-SNAPSHOT` versions to Sonatype. The workflow is setup to run either manually (with `workflow_dispatch`) or on every merge.
- [Publish Release](.github/workflows/publish-release.yaml) - Will publish a new release version of the libraries to Maven Central on tag pushes. You can trigger the workflow also manually if needed.

### To Jitpack

If you're using [JitPack](https://jitpack.io/), you don't need any further configuration and you can just configure the repo on JitPack.

You probably want to disable the [Publish Snapshot] and [Publish Release](.github/workflows/publish-release.yaml) workflows (delete the files), as Jitpack will take care of that for you.

## Project Structure

The project includes three sub-projects, each in their own subdirectories:

- **`app`:** The source for the final Android application.

The following additional top-level directories configure & support building the app & projects:

- **`buildSrc`:** Contains shared Gradle logic as [precompiled script plugins](https://docs.gradle.org/current/userguide/custom_plugins.html#sec:precompiled_plugins)
- **`config`:** Contains the [Detekt configuration file](https://detekt.dev/docs/introduction/configurations/).
- **`gradle`:** Contains Gradle Configuration files such as the Gradle Version Catalog and the [Gradle Wrapper](https://docs.gradle.org/current/userguide/gradle_wrapper.html).

Finally, the following hidden top-level directories provide functionality for specific development systems:

- **`.github`:** Defines the [Github Actions](https://github.com/features/actions) CI tasks and templates for new pull requests, issues, etc.
- **`.idea`:** Sets common initial project settings when the project is opened in [Android Studio](https://developer.android.com/studio) or [IntelliJ IDEA](https://www.jetbrains.com/idea/).

## Contributing 🤝

Feel free to open a issue or submit a pull request for any bugs/improvements.