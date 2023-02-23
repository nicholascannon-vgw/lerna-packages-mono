# Lerna Node Packages Spike

Spike using Lerna to publish a mono-repo of packages.

## Interesting links

-   https://docs.github.com/en/packages/quickstart
-   https://lerna.js.org/docs/features/version-and-publish
-   https://github.com/lerna/lerna/tree/main/libs/commands/publish#readme
-   https://github.com/lerna/lerna/tree/main/libs/commands/run#readme

## Pipeline

An example pipeline can be found in `./codefresh/build-and-publish.yml`.

Notes:

-   Build and test steps use `lerna exec` and `lerna run` to run install deps and npm scripts respectively, only for packages that have a diff in the current commit (`--since HEAD~1`)
-   Deploy step uses `lerna publish` and the independent versioning setting to only deploy packages for which a version does not exist in the registry. This means we must bump the version to publish the package.
-   If you create a diff in a package and don't bump the version, the `Package` step in the build pipeline will fail if that version is already published to the registry
