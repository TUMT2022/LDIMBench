
### File level Interface

The file level interface is the low level interface of the benchmark suite.
It is designed to make it easy to implement the interface in any environment (docker, local, remote).

#### Input:

```
./input
 | -- demands/
 |     | -- <sensorname>.csv
 | -- pressures/
 |     | -- <sensorname>.csv
 | -- flows/
 |     | -- <sensorname>.csv
 | -- levels/
 |     | -- <sensorname>.csv
 | -- model.inp            # The water network model
 | -- dma.json             # Layout of the district metering zones
 | -- options.yml # Options for the algorithm (e.g. training and evaluation data timestampy, stage of the algorithm [training, detection_offline, detection_online] and goal (detection, localization), hyperparameters, etc.)
```

> We trust the implementation of the Leakage detection method to use the correct implementation for each stage (e.g. doing online detection if told to instead of offline detection)

The following assumptions are made about the input data:

- the model is the leading datasource (meaning any sensor names in the other files must be present in the model)
- the model is a valid EPANET model

Maybe:

- the model might contain existing patterns

The following assumptions are not made:

- Timestamps are not required to be the same for all input files, to make it possible for the methods to do their own resample and interpolation of the data

#### Output:

```
./output
 | -- leaks.csv    # The leaks found by the algorithm

```