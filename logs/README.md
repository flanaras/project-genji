# Logs

Scripts to parse and extract information from files gathered from [../benchmarking/README.md](../benchmarking/README.md).

## Files

* create_preprocessing-caffe-log: Requires as the parameter Caffe's log.
This parses Caffe's output and collects the time, batch_time, read_time and transform_time, in the csv format.
Run this compiled in debug mode or use the branch with manual instrumentations.
If Caffe is used from any other sources than the manual instrumentation branch, then the corresponding lines have to be changed (line 3).

* parse-nvidia: Requires the nvidia.log file.
Parses the output of nvidia-smi pmon and converts it to a csv file.

* transform-cpu-gpu-timings: Parses Caffe's output in the csv format, including the manual instrumentation values.

* transform-cpu-gpu-timings-my: Same as transform-cpu-gpu-timings but for "my version" (DTT) of Caffe.

* rename-b: this script renames the preprocessed files and appends some text in the end of the files.

* do-both: runs both transform-cpu-gpu-timings and create_preprocessing-caffe-log
