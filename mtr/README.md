# proxysql_scheduler automated functional tests

## Background
This directory contains tests that can be executed by standard PXC MTR framework.
We found that automating proxysql_scheduler tests is needed to make them repeatable and much faster to execute. Standard MTR famework which allows interactions with mysql daemons, clients and arbitrary software is used to achieve this goal.
The idea is to not modify the framework already existing in PXC repository. We provide dedicated MTR suite for proxysql_scheduler testing together with several convenience include files for common tasks.

## How to use
1. Install and start ProxySQL service.
Admin credentials: admin/admin
Admin port: 6032
Connection port: 6033
2. Next step is to have PXC binaries,  tests and MTR framework. They can be installed from PXC package or build from sources.
3. Clone `proxysql_scheduler` project
4. Inside PXC mtr test suites create link to the `proxysql` directory
5. Environment variable PROXYSQL_SCHEDULER_SCRIPT pointing to `proxysql_scheduler` binary
`export PROXYSQL_SCHEDULER_SCRIPT=/path/to/proxysql_scheduler`
6. Temporary solution (will be removed when we have command line scheduler parameters).
Environment variable PROXYSQL_SCHEDULER_CONFIG_DIR pointing to the directory where proxy_scheduler config files used by tests are located.
`export PROXYSQL_SCHEDULER_CONFIG_DIR=/some/path/mysql-test/suite/proxysql/t
7. Execute mtr tests
`./mtr writer_to_maintenance reader_to_maintenance --parallel=1`
or
`./mtr --suite=proxysql --parallel=1`

## Limitations
1. Tests cannot be executed in parallel because they use the same ProxySQL instance