# GitHub Actions for yarn (DEPRECATED)

*NOTE: This is basically unnecessary. You can simply just use the `node:13-slim` or whatever container you like and just `run: yarn build` or whatever yarn command you wish in your GitHub Action. I will be archiving this repository.*

Example:

```
      - name: yarn install
        uses: docker://node:13-slim
        with:
          args: 'yarn install'
```


## OLD INFO - DO NOT USE

This Action for [yarn](https://yarnpkg.com/en/) enables arbitrary actions with the `yarn` command-line client. Uses the node 11 docker image as its base.

## Usage

An example workflow to test and then build only on `master`:

```
workflow "Main" {
  on = "push"
  resolves = ["Build"]
}

action "Install" {
  uses = "docker://justinharringa/actions-yarn:master"
  args = "install"
  env = {
    CI = "true"
  }
}

action "Test" {
  needs = "Install"
  uses = "docker://justinharringa/actions-yarn:master"
  args = "test"
  env = {
    CI = "true"
  }
}

action "Filters for GitHub Actions" {
  needs = ["Test"]
  uses = "actions/bin/filter@b2bea07"
  args = "branch master"
}

action "Build" {
  needs = "Filters for GitHub Actions"
  uses = "docker://justinharringa/actions-yarn:master"
  args = "build"
  env = {
    CI = "true"
  }
}
```

## Credit
Credit goes to [CultureHQ and their original repo](https://github.com/CultureHQ/actions-yarn)
