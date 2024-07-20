# HPL

High-Performance Linpack benchmark.

## Source

A reference implementation is available from the Netlib repository and can be
reached through the Top500 web page at

https://www.top500.org/project/linpack.

Users are free to use optimized proprietary High-Performance Linpack
versions that comply with the Top500 list rules.

## Building

Not specified.

All modifications in accordance with the rule of the Top500 list are admissible.

## Execution

All modifications in accordance with the rule of the Top500 list are admissible.

The reference HPL can be executed by

```
cd bin/<arch>
srun -n 4 xhpl
```

The parameters can be tuned by modifying the input file `bin/HPL.dat`.

## Execution with JUBE

The HPL benchmark can be executed with the provided JUBE script. Make sure, you have `JUBE`, `Python` and `sympy` loaded:

```
ml JUBE Python SciPy-bundle sympy
jube run hpl.xml [--tag tags...]
jube continue benchmarks_juwelsbooster # wait/repeat until all steps are done
jube result -a benchmarks_juwelsbooster
```

The following tags are available:

|      Tag      |                            Purpose                             |
|---------------|----------------------------------------------------------------|
| `scaling`     | scaling run                                                    |
| `nodelist`    | test all nodes in nodelist (e.g. screening)                    |
| `maint`       | test all nodes in given partition (use together with nodelist) |
| `hold`        | submit jobs with --hold                                        |
| `singlenode`  | run only on 1 node                                             |
| `iteration`   | run multiple iteration                                         |
| `binary`      | use pre-compiled binary (copy binary to `bin/xhpl`)             |
| `gpu`         | use GPUs                                                       |
| `reservation` | runs jobs in reservation (modify reservation name in script)   |
| `fullsystem`  | run on full system                                             |

Example: Running a precompiled binary (`bin/xhpl`; modify path in JUBE script if needed) on the GPUs on a single node requires using the following tags `--tag/-t`:

```
jube run hpl.xml --tag singlenode gpu binary
```

## Verification

As required for the Top500 list.

## Results

The HPL benchmarks outputs the performance of the benchmark in GFLOP/s.

Using JUBE, a result table similar to the following one will be generated, with the HPL metric as `pat_perf_all[Gflops]`. 

| nodes | taskspernode | threadspertask |   hpl_N |   pat_N | pat_perf_all [Gflops] | pat_perf_avg_node [Gflops] |
|-------|--------------|----------------|---------|---------|----------------------|---------------------------|
|    64 |            4 |             12 | 1141344 | 1141344 |            1.746e+06 |                 2.728e+04 |

## Commitment

Candidates are requested to provide three values:

* HPL performance and power consumption on a single Compute Node
* HPL performance and power consumption on sixteen Compute Nodes
* HPL performance and power consumption on the full system, i.e., (almost) all Compute Nodes, as used for the Top500 list submission

The power consumption is to be given in accordance with the Green500 rules.

The execution no the full system is used for the quantitative assessment.
