# check_elasticsearch_snapshot

Check Elasticsearch Snapshot-Backup (SLM)

A basic Nagios/Icinga plugin to check the status and age of an Elasticsearch snapshot.

By default all Snapshots are checked for status and age. You can also specify a specific repository to check.

## Installation

### Requirements

* Python 3.4+
* Python requests package
  * pip install requests
  * RedHat/CentOS
    * python34-requests.noarch

### Plugin Installation

* Download check_elasticsearch_snapshot to your plugins directory (nagios/icinga)
* Add/Import the CheckCommand configuration

## Usage (Help)

```bash
$ ./check_elasticsearch_snapshot --help
```

```bash
usage: This plugin checks the Elasticsearch snapshots for either all or a specific repository. It will test the age of any successful snapshot, using the newest in each repository.
  [-h] [-m SCHEME] -s SERVER -p PORT [--userauth USERAUTH] [--basicauth BASICAUTH] [--username USERNAME] [--password PASSWORD] [--subfolder SUBFOLDER] -w WARNING -c CRITICAL [-r REPOSITORY]
       [--allow-partial]

optional arguments:
  -h, --help            show this help message and exit
  -m SCHEME, --scheme SCHEME
                        scheme (http/https defaults to http)
  -s SERVER, --server SERVER
                        server
  -p PORT, --port PORT  port
  --userauth USERAUTH   userauth
  --basicauth BASICAUTH
                        basicauth
  --username USERNAME   username
  --password PASSWORD   password
  --subfolder SUBFOLDER
                        subfolder
  -w WARNING, --warning WARNING
                        warning time (ms or suffixed with {s,m,h,d,w})
  -c CRITICAL, --critical CRITICAL
                        critical time (ms or suffixed with {s,m,h,d,w})
  -r REPOSITORY, --repository REPOSITORY
                        repository
  --allow-partial       Treat PARTIAL snapshots as SUCCESS`
```

### Thresholds

The following suffixes can be used; an entirely numeric value is considered as milliseconds.
* s - seconds
* m - minutes
* h - hours
* d - days
* w - weeks
#### Threshold Examples
* `3h` is 3 hours
* `1.25d` is 1 day and 6 hours

### Examples

```
$ ./check_elasticsearch_snapshot -m https -s <hostname_fqdn> -p 9200 --basicauth "<digest>" -r <repo_name> -w 2d -c 2.5d
```
`OK - Most current Repository/Snapshot: my_nfs_repo1/nightly-snap-2021.05.05-qlb0399gtk6ohwnwazazba 2021-05-05T01:31:35.898Z | newest_age_seconds=24569.743655517577 newest_age_days=0.284372033049972`

## Source

Icinga: https://exchange.icinga.com/leeclemens/check_elasticsearch_snapshot
Github: https://github.com/leeclemens/check_elasticsearch_snapshot
