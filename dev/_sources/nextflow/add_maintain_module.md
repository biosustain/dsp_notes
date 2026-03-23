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
nf-core modules lint -d . onsite   
nf-core modules lint --fix -d . onsite    

nf-test test --profile docker modules/bigbio/onsite/tests/main.nf.test
nf-test test --profile docker modules/bigbio/onsite/tests/main.nf.test --update-snapshot
# nf-test is also available via nf-core tools cli:
nf-core modules test -d . --profile docker --update onsite
```

- on snapshots: [link](https://www.nf-test.com/docs/assertions/snapshots/)
