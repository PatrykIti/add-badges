<h1 align="center">This repo is forked from <a href="https://github.com/wow-actions/add-badges">wow-actions/add-badges</a></h1>
<p>The changes made to the code:<br />
  <ol>
    <li>Added 'ref' parameter to choose branch where badges will be commited</Li>
    <li>Changing workflows for building packages, tagging and release because previous one were not working</li>
  </ol>
</p>

<h1 align="center">Add Badges</h1>
<p align="center">
    Automatically add badges on <a href="https://shields.io">shield.io</a> to <code>README.md</code> for your repository
</p>

<!-- [START BADGES] -->
<!-- Please keep comment here to allow auto update -->
<p align="center">
  <a href="https://github.com/PatrykIti/add-badges/blob/master/LICENSE"><img src="https://img.shields.io/github/license/PatrykIti/add-badges?style=flat-square" alt="MIT License" /></a>
  <a href="https://www.typescriptlang.org"><img src="https://img.shields.io/badge/language-TypeScript-blue.svg?style=flat-square" alt="Language" /></a>
  <a href="https://github.com/PatrykIti/add-badges/pulls"><img src="https://img.shields.io/badge/PRs-Welcome-brightgreen.svg?style=flat-square" alt="PRs Welcome" /></a>
  <a href="https://github.com/PatrykIti/add-badges/actions/workflows/release.yml"><img src="https://img.shields.io/github/actions/workflow/status/PatrykIti/add-badges/release.yml?logo=github&style=flat-square" alt="build" /></a>
</p>
<!-- [END BADGES] -->

## Usage

1. Specify the location of badges in your `README.md` file by adding some comments:

```md
<!-- [START BADGES] -->
<!-- [END BADGES] -->
```

2. Create a workflow file such as `.github/workflows/add-badges.yml` in your repository.

<!-- [START BADGES 1] -->
<!-- Please keep comment here to allow auto update -->
[![MIT License](https://img.shields.io/github/license/PatrykIti/add-badges?style=flat-square)](https://github.com/PatrykIti/add-badges/blob/master/LICENSE)
[![Language](https://img.shields.io/badge/language-TypeScript-blue.svg?style=flat-square)](https://www.typescriptlang.org)
[![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-brightgreen.svg?style=flat-square)](https://github.com/PatrykIti/add-badges/pulls)
[![build](https://img.shields.io/github/actions/workflow/status/PatrykIti/add-badges/release.yml?logo=github&style=flat-square)](https://github.com/PatrykIti/add-badges/actions/workflows/release.yml)
<!-- [END BADGES 1] -->

```yml
name: Add Badges
on:
  push:
    branches:
      - master
jobs:
  run:
    runs-on: ubuntu-latest
    steps:
      - uses: PatrykIti/add-badges@v1
        env:
          repo_url: ${{ github.event.repository.html_url }}
          repo_name: ${{ github.event.repository.name }}
          repo_owner: ${{ github.event.repository.owner.login }}
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          badges: |
            [
              {
                "badge": "https://img.shields.io/github/license/${{ env.repo_owner }}/${{ env.repo_name }}?style=flat-square",
                "alt": "MIT License",
                "link": "${{ env.repo_url }}/blob/master/LICENSE"
              },
              {
                "badge": "https://img.shields.io/badge/language-TypeScript-blue.svg?style=flat-square",
                "alt": "Language",
                "link": "https://www.typescriptlang.org"
              },
              {
                "badge": "https://img.shields.io/badge/PRs-Welcome-brightgreen.svg?style=flat-square",
                "alt": "PRs Welcome",
                "link": "${{ env.repo_url }}/pulls"
              },
              {
                "badge": "https://img.shields.io/github/workflow/status/${{ env.repo_owner }}/${{ env.repo_name }}/Release?logo=github&style=flat-square",
                "alt": "build",
                "link": "${{ env.repo_url }}/actions/workflows/release.yml"
              }
            ]
```

We also can add multi-line badges with nested array.

<!-- [START BADGES 2] -->
<!-- Please keep comment here to allow auto update -->
<p align="center">
  <a href="https://github.com/PatrykIti/add-badges/blob/master/LICENSE"><img src="https://img.shields.io/github/license/PatrykIti/add-badges?style=flat-square" alt="MIT License" /></a>
  <a href="https://www.typescriptlang.org"><img src="https://img.shields.io/badge/language-TypeScript-blue.svg?style=flat-square" alt="Language" /></a>
  <a href="https://github.com/PatrykIti/add-badges/pulls"><img src="https://img.shields.io/badge/PRs-Welcome-brightgreen.svg?style=flat-square" alt="PRs Welcome" /></a>
</p>

<p align="center">
  <a href="https://github.com/PatrykIti/add-badges/actions/workflows/release.yml"><img src="https://img.shields.io/github/actions/workflow/status/PatrykIti/add-badges/release.yml?logo=github&style=flat-square" alt="build" /></a>
</p>
<!-- [END BADGES 2] -->

```yml
name: Add Badges
on:
  push:
    branches:
      - master
jobs:
  run:
    runs-on: ubuntu-latest
    steps:
      - uses: PatrykIti/add-badges@v1
        env:
          repo_url: ${{ github.event.repository.html_url }}
          repo_name: ${{ github.event.repository.name }}
          repo_owner: ${{ github.event.repository.owner.login }}
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          ref: ${{ github.event.pull_request.head.ref }}
          center: true
          badges: |
            [
              [
                {
                  "badge": "https://img.shields.io/github/license/${{ env.repo_owner }}/${{ env.repo_name }}?style=flat-square",
                  "alt": "MIT License",
                  "link": "${{ env.repo_url }}/blob/master/LICENSE"
                },
                {
                  "badge": "https://img.shields.io/badge/language-TypeScript-blue.svg?style=flat-square",
                  "alt": "Language",
                  "link": "https://www.typescriptlang.org"
                },
                {
                  "badge": "https://img.shields.io/badge/PRs-Welcome-brightgreen.svg?style=flat-square",
                  "alt": "PRs Welcome",
                  "link": "${{ env.repo_url }}/pulls"
                }
              ],
              [
                {
                  "badge": "https://img.shields.io/github/workflow/status/${{ env.repo_owner }}/${{ env.repo_name }}/Release?logo=github&style=flat-square",
                  "alt": "build",
                  "link": "${{ env.repo_url }}/actions/workflows/release.yml"
                }
              ]
            ]
```

## Inputs

Various inputs are defined to let you configure the action:

> Note: [Workflow command and parameter names are not case-sensitive](https://docs.github.com/en/free-pro-team@latest/actions/reference/workflow-commands-for-github-actions#about-workflow-commands).

| Name              | Description                                           | Default                                          |
|-------------------|-------------------------------------------------------|--------------------------------------------------|
| `GITHUB_TOKEN`    | The GitHub token for authentication                   | N/A                                              |
| `badges`          | Badges to add                                         | N/A                                              |
| `path`            | The file path to add badges                           | `'README.md'`                                    |
| `ref`             | The branch name                                       | `'master'`                                       |
| `center`          | Should center align the badges or not                 | `false`                                          |
| `commit_message`  | Commit message                                        | `'docs: add badges [skip ci]'`                   |
| `committer_name`  | The name of the author or committer of the commit.    | `'github-actions[bot]'`                          |
| `committer_email` | The email of the author or committer of the commit.   | `'github-actions[bot]@users.noreply.github.com'` |
| `opening_comment` | The comment to match the start line of badges section | `'<!-- [START BADGES] -->'`                      |
| `closing_comment` | The comment to match the end line of badges section   | `'<!-- [END BADGES] -->'`                        |

## License

The scripts and documentation in this project are released under the [MIT License](LICENSE).
