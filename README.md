# vcpus

Estimates the allocated cpus count on a host or in a container for
which cgroups CPUs requirements and limits have been defined.

Can be used as a replacement for the ``nproc`` tool from ``GNU coreutils``
when actual CPUs share matters.

This tool works under Linux systems, on other systems no estimation
is performed and the system returned CPU count is used.

The script uses the cgroup information in order to get:
- cardinality of CPUs set
- allocated CPUs shares (generally used for specifying requirements)
- ratio of CPUs quota per period (generally used for specifying limits)

Then, with the system returned number of CPUs as an upperbound,
an estimation of the number of CPUs allocated to the container is performed
from these allocations.

For instance in a container executed with CPUs requirements set to 2 vCPUs
and limit set to 4 vCPUs running on a 8 cores host, the following is returned:

    vcpus  # same as: vcpus --allocated
    2
    vcpus --limit
    4
    vcpus --cpu-set
    8
    vcpus --cpu-shares
    2
    vcpus --cpu-quota
    4
    vcpus --nprocs # the host returned configuration
    8

The command executed without argument may be used as a replacement for the
``nproc`` command. For instance when executing parallel build tasks:

    # In some build system around
    make -j $(vcpus) all


# Installation

Download the self contained ``vcpus`` python script from the releases page: https://github.com/guillon/repo-mirror/releases
For instance doewnload ``v1.0.1`` version with:

    curl -L -o vcpus  https://github.com/guillon/vcpus/releases/download/v1.0.1/vcpus
    chmod +x vcpus
    ./vcpus --help

Or install with setup tools, for instance in user environment (``~/.local/bin``) with:

    ./setup.py install --user
    vcpus --help

# Licence

This is free and unencumbered software released into the public domain.
