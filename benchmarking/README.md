# Benchmarking

A set of scripts to gather information from Caffe's execution.

## Files

* start-logging: Invokes train and clean-up scripts.

* train: The script to execute that sets up everything for the training part. Creates a folder at `~/logs` for the output of all measurements. Creates a subfolder within that contains all information from a single execution.

* clean-up: Cleans up the ram of the computer from left over cache.

* caffe-stats: Collects cpu, ram, page fault, etc. measurements for Caffe.

* nvidia-stats: Collects GPU stats.

* parse_files: Invokes parsing scripts.


## Folders

* library: Other scripts that were developed but not used.

