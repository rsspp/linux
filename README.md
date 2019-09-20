This is a repository containing a modified version of the 5.1.5 Linux kernel to support features of RSS++:

- Support for giving the "hash" from RSS to a BPF XDP program. Just to avoid recomputing the hash in software.
- SO_AUTOMIGRATE allows to migrate a thread doing a read on a socket to the core where the last packet was received. Of course, this is to be used in a sharding context where all packets of the same flow are handled on the same core. With RSS++, flows may be migrated, and the thread will therefore migrate with it at its next read call.
- SO_SHARDED allows to use per-core flow table. Unfortunately this did not lead to the improvements we wanted, because there are still thousands locks and source of contention in the kernel. Mostly, buffer recycling should be sharded too. Sadly, this is most of the modifications in this repository. The other features do not depend on SO_SHARDED though.

You can obtain a patch using `git diff v5.1.5` 

Original README
===============

Linux kernel
============

There are several guides for kernel developers and users. These guides can
be rendered in a number of formats, like HTML and PDF. Please read
Documentation/admin-guide/README.rst first.

In order to build the documentation, use ``make htmldocs`` or
``make pdfdocs``.  The formatted documentation can also be read online at:

    https://www.kernel.org/doc/html/latest/

There are various text files in the Documentation/ subdirectory,
several of them using the Restructured Text markup notation.

Please read the Documentation/process/changes.rst file, as it contains the
requirements for building and running the kernel, and information about
the problems which may result by upgrading your kernel.
