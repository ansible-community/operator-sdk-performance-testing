# Operator SDK Performance Testing

[![CI](https://github.com/geerlingguy/operator-sdk-performance-testing/workflows/CI/badge.svg?branch=master)](https://github.com/geerlingguy/operator-sdk-performance-testing/actions?query=workflow%3ACI)

This repository contains some automation code to assist with performance testing for some aspects of the Kubernetes [Operator SDK](https://github.com/operator-framework/operator-sdk).

## Running the test

TODO:

  1. Install [Kind](https://kind.sigs.k8s.io/docs/user/quick-start/).
  1. Install dependencies: `pip3 install molecule openshift docker`
  1. Set the operator to test (one of `ansible`, `go`, or `helm`): `export operator_under_test=ansible`
  1. Run: `molecule test`

## Author

This repository was created in 2020 by [Jeff Geerling](https://www.jeffgeerling.com).
