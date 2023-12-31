# Evaluation 2023
Using [home-baked benchmarking suite](https://github.com/d702e20/bench-solver), which takes a CSV of name, model, formula declarations and outputs a CSV with the following details depending on which that apply (e.g. threads for PRISM does not make sense, similarly for search-strategy):

- name, model, formula
- time\_s
- threads
- memory\_MB
- total\_reported (secs)
- construction (secs)
- checking (secs)

Note that memory-measurements are flawed due to limitations with `ru_maxrss`.

## Legacy Criterion evaluation
Using Criterion with input to bench on a case-study (LCGS + one query) while varying worker-threads between 1 and 32.
Output from Criterion is gathered into folderes for each case-study. Entire stdout and stdin are recorded in {JOBID}.err/.out.

Stdout contains a line (or two if name needs wrapping) for each sub-test of a case-study. Left and right values are lower- and upper time-bounds, while the middle value is the average over at least 100 samples:
```
~ cat bench-6030006.out
rc3_threads/1           time:   [52.160 s 52.181 s 52.204 s]
Found 2 outliers among 100 measurements (2.00%)
  1 (1.00%) high mild
  1 (1.00%) high severe
rc3_threads/2           time:   [27.420 s 27.489 s 27.555 s]
rc3_threads/3           time:   [18.882 s 18.944 s 19.005 s]
```

Runs are organised with prepended type (bfs, dfs, dependency_heuristic, etc) and its SLURM jobid for tracing. Use `tar -xvf {TYPE}-{JOBID}.tar.gz` to access Criterion reports.

