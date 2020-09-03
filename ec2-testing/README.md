# EC2 Test Environment

This directory contains a set of playbooks which builds an Amazon EC2 instance, runs the Operator SDK performance benchmarks on it, and destroys the instance.

The playbooks build all the required components (including VPC, networking, security groups, etc.), and you can modify the `vars/main.yml` file to use different defaults if you'd like (e.g. a different `aws_profile` if you don't have a profile named `aworks`).

## Usage

Make sure you have `boto` installed locally: `pip3 install boto`.

Install requirements:

```
ansible-galaxy install -r requirements.yml
```

Build the environment:

```
$ ansible-playbook build.yml
```

Run the benchmarks in the environment:

```
$ ansible-playbook benchmark.yml
```

The results for all three operators are output in the molecule logs stored inside this directory, with the names `result-[ansible|go|helm].txt`, respectively.

## Cleanup

Once you're finished benchmarking, run the `destroy.yml` playbook to destroy the test environment:

```
$ ansible-playbook destroy.yml
```
