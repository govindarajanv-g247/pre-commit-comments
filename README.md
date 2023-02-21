# pre-commit-comments


Make sure `pre-commit` is [installed](https://pre-commit.com#install).

Create a blank configuration file at the root of your repo, if needed:

```console
touch .pre-commit-config.yaml
```

Add a new repo entry to your configuration file:

```yaml
repos:

# - repo: ...

  - repo: https://github.com/compilerla/conventional-pre-commit
    rev: <git sha or tag>
    hooks:
      - id: conventional-pre-commit
        stages: [commit-msg]
        args: [] # optional: list of Conventional Commits types to allow e.g. [feat, fix, ci, chore, test]
```

Install the `pre-commit` script:

```console
pre-commit install --hook-type commit-msg
```

Make a (normal) commit :x::

```console
$ git commit -m "add a new feature"

[INFO] Initializing environment for ....
Conventional Commit......................................................Failed
- hook id: conventional-pre-commit
- duration: 0.07s
- exit code: 1

[Bad Commit message] >> add a new feature

Your commit message does not follow Conventional Commits formatting
https://www.conventionalcommits.org/

Conventional Commits start with one of the below types, followed by a colon,
followed by the commit message:

    build chore ci docs feat fix perf refactor revert style test

Example commit message adding a feature:

    feat: implement new API

Example commit message fixing an issue:

    fix: remove infinite loop

Optionally, include a scope in parentheses after the type for more context:

    fix(account): remove infinite loop
```

Make a (conventional) commit :heavy_check_mark::

```console
$ git commit -m "feat: add a new feature"

[INFO] Initializing environment for ....
Conventional Commit......................................................Passed
- hook id: conventional-pre-commit
- duration: 0.05s
```


## Install with pip

`conventional-pre-commit` can also be installed and used from the command line:

```shell
pip install conventional-pre-commit
```

Then run the command line script:

```shell
conventional-pre-commit [types] input
```

Where `[types]` is an optional list of Conventional Commit types to allow (e.g. `feat fix chore`)

And `input` is a file containing the commit message to check:

```shell
conventional-pre-commit feat fix chore ci test .git/COMMIT_MSG
```