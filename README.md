<!--
# SPDX-License-Identifier: Apache-2.0
# SPDX-FileCopyrightText: 2025 The Linux Foundation
-->

# 🛠️ Verify Jupyter Notebooks

Validates Jupyter Notebooks with pytest and nbmake.

## python-notebook-test-action

## Usage Example

<!-- markdownlint-disable MD046 -->

```yaml
  steps:
    - name: "Verify Jupyter Notebooks"
      uses: lfreleng-actions/python-notebook-test-action@main
      with:
        python_version: "${{ env.python_version }}"
```

<!-- markdownlint-enable MD046 -->

## Inputs

<!-- markdownlint-disable MD013 -->

| Variable Name   | Required | Default | Description                                       |
| --------------- | -------- | ------- | ------------------------------------------------- |
| PYTHON_VERSION  | True     |         | Python version used to run tests                  |
| PERMIT_FAIL     | False    | False   | Continue even when one or more tests fails        |
| PATH_PREFIX     | False    |         | Directory location containing Python project code |
| PARALLEL_TESTS  | False    | False   | Parallel pytest/nbmake processes                  |
| NBMAKE_KERNEL   | False    | False   | Force nbmake to use a specific kernel             |
| INSTALL_KERNEL  | False    | False   | Install custom kernel before running tests        |

<!-- markdownlint-enable MD013 -->

## Implementation Details

Refer to the following Python tool documentation: [nbmake](https://github.com/treebeardtech/nbmake)

## Notes

A wildcard search pattern under the PATH_PREFIX locates notebooks to test:

`path_prefix/**/*ipynb`

If this fails to locate any files, then the action will fail.

Parallel tests can speed up execution when large/complex notebooks are present.

Enabling INSTALL_KERNEL will invoke the following command before tests run:

```console
python -m ipykernel install --user --name [NBMAKE_KERNEL]
```

In this instance, you must set NBMAKE_KERNEL otherwise the action will fail.
