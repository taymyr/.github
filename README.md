# Taymyr GitHub integration

This repository contains a few configurations of GitHub features. For example a [Reusing workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows)

## Reusing Workflows

* [Mark Pull Request as Ready To Merge](#mark-pull-request-as-ready-to-merge)

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
