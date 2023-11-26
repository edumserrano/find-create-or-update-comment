# Find, create or update comment GitHub action

[![Test GitHub action](https://github.com/edumserrano/find-create-or-update-comment/actions/workflows/test-action.yml/badge.svg)](https://github.com/edumserrano/find-create-or-update-comment/actions/workflows/test-action.yml)
[![Test GitHub action from GH Marketplace](https://github.com/edumserrano/find-create-or-update-comment/actions/workflows/test-action-gh-marketplace.yml/badge.svg)](https://github.com/edumserrano/find-create-or-update-comment/actions/workflows/test-action-gh-marketplace.yml)
[![GitHub Marketplace](https://img.shields.io/badge/Marketplace-Find,%20create%20or%20update%20comment-blue.svg?colorA=24292e&colorB=0366d6&style=flat&longCache=true&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA4AAAAOCAYAAAAfSC3RAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAM6wAADOsB5dZE0gAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAAAERSURBVCiRhZG/SsMxFEZPfsVJ61jbxaF0cRQRcRJ9hlYn30IHN/+9iquDCOIsblIrOjqKgy5aKoJQj4O3EEtbPwhJbr6Te28CmdSKeqzeqr0YbfVIrTBKakvtOl5dtTkK+v4HfA9PEyBFCY9AGVgCBLaBp1jPAyfAJ/AAdIEG0dNAiyP7+K1qIfMdonZic6+WJoBJvQlvuwDqcXadUuqPA1NKAlexbRTAIMvMOCjTbMwl1LtI/6KWJ5Q6rT6Ht1MA58AX8Apcqqt5r2qhrgAXQC3CZ6i1+KMd9TRu3MvA3aH/fFPnBodb6oe6HM8+lYHrGdRXW8M9bMZtPXUji69lmf5Cmamq7quNLFZXD9Rq7v0Bpc1o/tp0fisAAAAASUVORK5CYII=)](https://github.com/marketplace/actions/find-create-or-update-comment)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](./LICENSE)
[![GitHub Sponsors](https://img.shields.io/github/sponsors/edumserrano)](https://github.com/sponsors/edumserrano)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Eduardo%20Serrano-blue.svg)](https://www.linkedin.com/in/eduardomserrano/)

- [Description](#description)
- [Why should you use this action ?](#why-should-you-use-this-action-)
- [Usage](#usage)
- [Action inputs](#action-inputs)
- [Dev notes](#dev-notes)

## Description

A composite [GitHub action](https://docs.github.com/en/actions/learn-github-actions/finding-and-customizing-actions) that can be used to find a GitHub Issue or Pull Request comment by a specified value and then update the comment if found or create it if not found.

## Why should you use this action ?

This is nothing more than a combination of the awesome work done by [Peter Evans](https://github.com/peter-evans). I'm combining the [find-comment](https://github.com/peter-evans/find-comment) and the [create-or-update-comment](https://github.com/peter-evans/create-or-update-comment) because I found that I end up using those actions together a lot of the time.

This is a implementation of what is described in [the docs for create-or-update-comment](https://github.com/peter-evans/create-or-update-comment#where-to-find-the-id-of-a-comment).

## Usage

```yml
- name: Update PR with test results
  uses: edumserrano/find-create-or-update-comment@v1
  with:
    issue-number: ${{ github.event.pull_request.number }}
    body-includes: '<!-- some-unique-id -->'
    comment-author: 'github-actions[bot]'
    body: | # can be a single value or you can compose text with multi-line values
      <!-- some-unique-id -->
      My awesome comment
    edit-mode: replace
```

The above usage example is using a trick to uniquely identify a comment with some text.

The GitHub comment contains a markdown comment using the `<!-- this is a comment -->` syntax. The markdown comment text should then be a unique identifier that we can use to search for. This way we can set unique ids for the comments but don't make them visible to the user/whoever is reading the comment on GitHub.

Also note that you can pass input from other steps into the `body` param by doing something like:

```yml
body: |
  <!-- some-unique-id -->
  ${{ steps.some-step-id.outputs.some-step-output }}
```

Alternatively to using an inline `body` you can use the `body-path` to specify a file to use.

## Action inputs

| Name                  | Description                                                                                                                       | Required                             | Default value                            |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------ | ---------------------------------------- |
| `token`               | GITHUB_TOKEN or a repo scoped PAT.                                                                                                | yes                                  | `github.token` (job token)               |
| `repository`          | The full name of the repository containing the issue or pull request where to find, create or update the comment.                 | yes                                  | `github.repository` (current repository) |
| `issue-number`        | The number of the issue or pull request in which to find, create or update the comment.                                           | yes                                  | -                                        |
| `body-includes`       | A string to search for in the body of comments. Cannot be used in conjunction with `body-regex`.                                  | yes, unless `body-regex` is used.    | -                                        |
| `body-regex`          | A regular expression to search for in the body of comments. Cannot be used in conjunction with `body-includes`.                   | yes, unless `body-includes` is used. | -                                        |
| `direction`           | Search direction, specified as `first` or `last`                                                                                  | no                                   | `first`                                  |
| `nth`                 | 0-indexed number, specifying which comment to update if multiple are found .                                                      | no                                   | 0                                        |
| `comment-author`      | The GitHub user name of the comment author.                                                                                       | false                                | -                                        |
| `body`                | The comment body. Cannot be used in conjunction with `body-path`.                                                                 | yes, unless `body-path` is used.     | -                                        |
| `body-path`           | The path to a file containing the comment body. Cannot be used in conjunction with `body`.                                        | yes, unless `body` is used.          | -                                        |
| `edit-mode`           | The mode when updating a comment, `replace` or `append`.                                                                          | false                                | `append`                                 |
| `append-separator`    | The separator to use when appending to an existing comment. (`newline`, `space`, `none`).                                         | false                                | `newline`                                |
| `reactions`           | A comma separated list of reactions to add to the comment (`+1`, `-1`, `laugh`, `confused`, `heart`, `hooray`, `rocket`, `eyes`). | false                                | -                                        |
| `reactions-edit-mode` | The mode when updating comment reactions, `replace` or `append`.                                                                  | false                                | `append`                                 |

## Dev notes

For notes aimed at developers working on this repo or just trying to understand it go [here](/docs/dev-notes/README.md).
