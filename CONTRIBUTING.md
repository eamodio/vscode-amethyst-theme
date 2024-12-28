# Contributing

👍🎉 First off, thanks for taking the time to contribute! 🎉👍

When contributing to this project, please first discuss the changes you wish to make via an issue before making changes.

Please note the [Code of Conduct](CODE_OF_CONDUCT.md) document, please follow it in all your interactions with this project.

## Your First Code Contribution

Unsure where to begin contributing? You can start by looking through the [`help-wanted`](https://github.com/eamodio/vscode-amethyst-theme/labels/help%20wanted) issues.

### Getting the code

```
git clone https://github.com/eamodio/vscode-amethyst-theme.git
```

Prerequisites

- [Git](https://git-scm.com/)
- [NodeJS](https://nodejs.org/), `>= v22.11.0`
- [pnpm](https://pnpm.io/), `>= 9.x` (install using [corepack](https://nodejs.org/docs/latest-v20.x/api/corepack.html))

### Dependencies

From a terminal, where you have cloned the repository, execute the following command to install the required dependencies:

```
pnpm install
```

### Formatting

This project uses [prettier](https://prettier.io/) for code formatting. You can run prettier across the code by calling `pnpm run pretty` from a terminal.

To format the code as you make changes you can install the [Prettier - Code formatter](https://marketplace.visualstudio.com/items/esbenp.prettier-vscode) extension.

Add the following to your User Settings to run prettier:

```
"editor.formatOnSave": true,
```

### Bundling

To generate a VSIX (installation package) run the following from a terminal:

```
pnpm run package
```

### Debugging

#### Using VS Code

1. Open the `vscode-amethyst-theme` folder
2. Ensure the required [dependencies](#dependencies) are installed
3. Choose the `Launch Theme` launch configuration from the launch dropdown in the Debug viewlet and press `F5`.

## Submitting a Pull Request

Please follow all the instructions in the [PR template](.github/PULL_REQUEST_TEMPLATE.md).

## Publishing

### Stable Releases

Use the [prep-release](scripts/prep-release.js) script to prepare a new release. The script updates the [package.json](package.json) and [CHANGELOG.md](CHANGELOG.md) appropriately, commits the changes as `Bumps to v{major}.{minor}.{patch}`, and creates a `v{major}.{minor}.{patch}` tag which when pushed will trigger the CI to publish a release.

1. Ensure you are on the `main` branch and have a clean working tree
2. Ensure the [CHANGELOG.md](CHANGELOG.md) has been updated with the release notes
3. Run `pnpm run prep-release` and enter the desired `{major}.{minor}.{patch}` version when prompted
4. Review the `Bumps to v{major}.{minor}.{patch}` commit
5. Run `git push --follow-tags` to push the commit and tag

Pushing the `v{major}.{minor}.{patch}` tag will trigger the [Publish Stable workflow](.github/workflows/cd-stable.yml) to automatically package the extension, create a [GitHub release](https://github.com/eamodio/vscode-amethyst-theme/releases/latest), and deploy it to the [VS Marketplace](https://marketplace.visualstudio.com/items?itemName=amodio.amethyst-theme).

If the action fails and retries are unsuccessful, the VSIX can be built locally with `pnpm run package` and uploaded manually to the marketplace. A GitHub release can also be [created manually](https://github.com/eamodio/vscode-amethyst-theme/releases/new) using `v{major}.{minor}.{patch}` as the title and the notes from the [CHANGELOG.md](CHANGELOG.md) with the VSIX attached.

### Pre-releases

The [Publish Pre-release workflow](.github/workflows/cd-pre.yml) is automatically run every AM unless no new changes have been committed to `main`. This workflow can also be manually triggered by running the `Publish Pre-release` workflow from the Actions tab, no more than once per hour (because of the versioning scheme).
