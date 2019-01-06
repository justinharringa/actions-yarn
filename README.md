# GitHub Actions for yarn

This Action for [yarn](https://yarnpkg.com/en/) enables arbitrary actions with the `yarn` command-line client. Uses the node 11 docker image as its base.

## Usage

An example workflow to lint and test:

```
workflow "Main" {
  on = "push"
  resolves = ["Build"]
}

action "Install" {
  uses = "docker://justinharringa/actions-yarn:master"
  args = "install"
}

action "Test" {
  uses = "docker://justinharringa/actions-yarn:master"
  args = "test"
}

action "Filters for GitHub Actions" {
  needs = ["Test", "Install"]
  uses = "actions/bin/filter@b2bea07"
  args = "branch master"
}

action "Build" {
  needs = "Filters for GitHub Actions"
  uses = "docker://justinharringa/actions-yarn:master"
  args = "build"
}
```

## Credit
Credit goes to [CultureHQ and their original repo](https://github.com/CultureHQ/actions-yarn)
