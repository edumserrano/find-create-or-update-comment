# Dev notes

## Composite GitHub action

This repo provides a composite action. See the [docs](https://docs.github.com/en/actions/creating-actions/creating-a-composite-action) for more information on how to build a composite action.

## GitHub Workflows

For more information about the GitHub workflows configured for this repo go [here](/docs/dev-notes/workflows/README.md).

## GitHub marketplace

This action is published to the [GitHub marketplace](https://github.com/marketplace/actions/nuget-push).

**Currently there is no workflow setup to publish this action to the marketplace. The publishing act is a manual process following the instructions below.**

When publishing a new version:

- create a new tag (like v1.0.4) for the release and update the latest major tag (like v1) to the same commit as the new tag.

From here on you can follow the instruction at [how to publish or remove an action from the marketplace](https://docs.github.com/en/actions/creating-actions/publishing-actions-in-github-marketplace).


