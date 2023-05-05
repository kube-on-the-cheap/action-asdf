# action-asdf

This action helps set up an environment using the [asdf version management](https://asdf-vm.com/) tool. It uses GitHub caching to be efficient and fast.

## Features

* The cache is built for a `.tool-versions` content and reused across branches
* Fast execution on cache-hit (~10 seconds)
* Explicit notices if requirements are missing (`.tool-versions` missing or invalid)
* Can execute `pre-commit` as a post-setup step

## Usage

```yaml
name: pre-commit checks
on:
  push:           #  <-- If you run on push to main, it will build the cache under
    branches:     #      the main/ branch ref and make it reusable for any non-changed
      - main      #      other branch
  pull_request:
    branches:
      - main

jobs:
  pre-commit:
    runs-on: ubuntu-latest
    steps:
      - uses: kube-on-the-cheap/action-asdf@v0.1.5
        with:
          run-pre-commit: true
```

## Inputs

<!-- AUTO-DOC-INPUT:START - Do not remove or modify this section -->

| INPUT               | TYPE   | REQUIRED | DEFAULT   | DESCRIPTION                                                                                                               |
| ------------------- | ------ | -------- | --------- | ------------------------------------------------------------------------------------------------------------------------- |
| force-cache-refresh | string | false    | `"false"` | Force the invalidation and refresh of <br>the cache                                                                       |
| python-version      | string | false    | `"3.11"`  | The Python version to install                                                                                             |
| run-pre-commit      | string | false    | `"false"` | Run pre-commit after setup                                                                                                |
| target-all-files    | string | false    | `"false"` | Run checks on all files in <br>the repo. Defaults to 'false' to <br>account only for the changed file <br>in this branch. |

<!-- AUTO-DOC-INPUT:END -->

## Outputs

None
