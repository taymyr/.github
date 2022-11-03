# Taymyr GitHub integration

This repository contains a few configurations of GitHub features. For example a [Reusing workflows](#reusing-workflows) or a [Release Drafter](#release-drafter).

## Release Drafter

See also [documentation](https://github.com/marketplace/actions/release-drafter).

**How to use**:

Create a `.github/workflows/release-drafter.yml` in the repository with the following:

```yaml
name: Release Drafter

on:
  push:
    branches:
      - main

jobs:
  update_release_draft:
    runs-on: ubuntu-latest
    steps:
      - uses: release-drafter/release-drafter@v5
        with:
          name: "<Module name> $RESOLVED_VERSION"
          config-name: release-drafts/patch-version.yml # located in .github/ in the default branch within this or the .github repo
          commitish: ${{ github.ref_name }}
          header: |
            Optional parameter. Use it if you want to prepend information above the release notes.  
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

As value of `config-file` parameter you can use the next variants:
* `release-drafts/patch-version.yml`
* `release-drafts/minor-version.yml`
* `release-drafts/major-version.yml`

## Reusing Workflows

See also [documentation](https://docs.github.com/en/actions/using-workflows/reusing-workflows).

* [Mark Pull Request as Ready To Merge](#mark-pull-request-as-ready-to-merge)
* [Sync Labels](#sync-labels)

### Mark Pull Request as Ready To Merge

This workflow is used for mark pull request as ready to merge and **should be last** in the workflows chain.

:warning: For using this workflow don't forget to configure the `needs` ([GA docs](https://docs.github.com/en/actions/using-workflows/advanced-workflow-features#creating-dependent-jobs)) attribute to make this workflow run last.

**Path**: [`workflows/rtm.yml`](.github/workflows/rtm.yml)

**Image**: [Ubuntu 20.04](https://github.com/actions/runner-images/blob/main/images/linux/Ubuntu2004-Readme.md)

**No Parameters**

**How to use**:

```yaml
needs: # Should be latest
  - "check-code-style"
  - "..."
  - "tests"
uses: taymyr/.github/.github/workflows/rtm.yml@v1
```

### Sync Labels

[Configuration of labels](.github/labels.yml) synchronize to all organization repositories by [Label Sync](https://github.com/marketplace/actions/label-sync) action. 

**Path**: [`workflows/sync-labels.yml`](.github/workflows/sync-labels.yml)

**Image**: [Ubuntu 20.04](https://github.com/actions/runner-images/blob/main/images/linux/Ubuntu2004-Readme.md)

**No Parameters**

**How to use**:

```yaml
uses: taymyr/.github/.github/workflows/sync-labels.yml@v1
```
