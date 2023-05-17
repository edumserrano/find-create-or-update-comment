# GitHub worflows

There is one workflow setup on this repo:

| Worflow                                                                         | Status and link                                                                                                                                                                                                                                                                     | Description                                                                           |
| ------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------ |
| [test-action](/.github/workflows/test-action.yml)                               | [![Test GitHub action](https://github.com/edumserrano/find-create-or-update-comment/actions/workflows/test-action.yml/badge.svg)](https://github.com/edumserrano/find-create-or-update-comment/actions/workflows/test-action.yml)                                                   | Builds and tests the GitHub action. Builds the action from this repo.                 |
| [test-action-gh-marketplace](/.github/workflows/test-action-gh-marketplace.yml) | [![Test GitHub action from GH Marketplace](https://github.com/edumserrano/find-create-or-update-comment/actions/workflows/test-action-gh-marketplace.yml/badge.svg)](https://github.com/edumserrano/find-create-or-update-comment/actions/workflows/test-action-gh-marketplace.yml) | Builds and tests the GitHub action. Uses the published version to GitHub Marketplace. |
| [pr-dependabot-auto-merge](/.github/workflows/pr-dependabot-auto-merge.yml)     | [![PR Dependabot auto merge](https://github.com/edumserrano/find-create-or-update-comment/actions/workflows/pr-dependabot-auto-merge.yml/badge.svg)](https://github.com/edumserrano/find-create-or-update-comment/actions/workflows/pr-dependabot-auto-merge.yml)                   | Automatically merges Dependabot PRs.                                                  |

## Workflows' documentation

- [test-action](/docs/dev-notes/workflows/test-action-workflow.md)
- [test-action-gh-marketplace](/docs/dev-notes/workflows/test-action-gh-marketplace-workflow.md)
- [pr-dependabot-auto-merge](/docs/dev-notes/workflows/pr-dependabot-auto-merge-workflow.md)
