# GitHub Actions for yarn

This Action for [yarn](https://yarnpkg.com/en/) enables arbitrary actions with the `yarn` command-line client. Uses the node 11 docker image as its base.

## Usage

An example workflow to lint and test:

```hcl
workflow "Main" {
  on = "push"
  resolves = ["Lint", "Test"]
}

action "Install" {
  uses = "docker://justinharringa/actions-yarn:latest"
  args = "install"
}

action "Lint" {
  needs = "Install"
  uses = "docker://justinharringa/actions-yarn:latest"
  args = "lint"
}

action "Test" {
  needs = "Install"
  uses = "docker://justinharringa/actions-yarn:latest"
  args = "test"
}
```

## Credit
Credit goes to [CultureHQ and their original repo](https://github.com/CultureHQ/actions-yarn)
