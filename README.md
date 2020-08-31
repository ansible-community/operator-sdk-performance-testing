# Operator SDK Performance Testing

[![CI](https://github.com/geerlingguy/operator-sdk-performance-testing/workflows/CI/badge.svg?branch=master)](https://github.com/geerlingguy/operator-sdk-performance-testing/actions?query=workflow%3ACI)

This repository contains some automation code to assist with performance testing for some aspects of the Kubernetes [Operator SDK](https://github.com/operator-framework/operator-sdk).

## Running the tests

  1. Install [Kind](https://kind.sigs.k8s.io/docs/user/quick-start/).
  1. Install Python dependencies: `pip3 install molecule openshift docker`
  1. Set the operator to test (one of `ansible`, `go`, or `helm`): `export operator_under_test=ansible`
  1. Run the benchmark with Molecule:

     ```
     OPERATOR_UNDER_TEST=ansible molecule test
     ```

You can set `OPERATOR_UNDER_TEST` to one of the following:

  - `ansible`
  - `go`
  - `helm`

It is best to run each benchmark individually, in a clean Kind cluster, instead of running one after the other, to ensure the benchmark is as accurate as possible.

## How it works

The Ansible playbook in `main.yml` uses a Kind cluster set up by Molecule to build and deploy the `OPERATOR_UNDER_TEST` into the cluster.

Then the playbook deploys the amount of Memcached CRs defined by `memcached_cr_count` in `config.yml` into the cluster.

Immediately after that, the playbook waits for all the expected Memcached instances to be up and running.

At the end of the playbook, Ansible's `profile_tasks` callback plugin reports back the timings of all the tasks. You can use these timings to benchmark the operators against each other.

## Author

This repository was created in 2020 by [Jeff Geerling](https://www.jeffgeerling.com).
