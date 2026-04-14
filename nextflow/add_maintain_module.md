# Add or update a module to nf-core/modules

- either to `nf-core/modules` for the nf-core community
- or to custom remotes as `bigbio/nf-modules` for internal use in `bigbio/quantms`
  (docs for custom remotes with nf-core tools
  [here](https://nf-co.re/docs/nf-core-tools/custom_remotes))

## Getting started

- [training of hello_nf-core](https://training.nextflow.io/latest/hello_nf-core/04_make_module/)
- [tutorial in nf-core docs](https://nf-co.re/docs/tutorials/nf-core_components/components)
- [module specifications](https://nf-co.re/docs/guidelines/components/modules)

## Lint and test

Here for example for a local module called `onsite` in `bigbio/nf-modules` repo:

```bash
# Run linting checks on the local directory (-d .) for the "onsite" module
# This validates structure, metadata, schema, and best practices compliance (nf-core gudelines)
nf-core modules lint -d . onsite

# More linting automatically fixing issues where possible (--fix)
# Useful for quick formatting corrections and minor standard violations
nf-core modules lint --fix -d . onsite

# Run nf-test unit tests for the onsite module using Docker profile
# Ensures the module behaves as expected in a containerized environment
nf-test test --profile docker modules/bigbio/onsite/tests/main.nf.test

# Run tests and update the expected output snapshots
# Use this when intended changes would modify outputs (e.g., after code refactoring)
nf-test test --profile docker modules/bigbio/onsite/tests/main.nf.test --update-snapshot

# A note on --update-snapshot, do not use it if you have not verified the outputs

# nf-test is also available via nf-core tools cli:
nf-core modules test -d . --profile docker --update onsite
```

- more on snapshots: [link](https://www.nf-test.com/docs/assertions/snapshots/)
