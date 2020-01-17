# Get an interactive node
```bash
qrsh -l h_rt=2:00:00,h_data=16G
```

# submitting a job
For qsub:
```text
-cwd (set working dir to the current one, when using relative path in script)
-V (Export all current variables to job environment)
-o [path] (specify path for job std output)
-e [path] (specify path for job error output)
-j [y/n] (if y, merge std & error output)
-hold_jid [job_id] (hold the job until specified job completes; essential for multi-step pipelines)
-m b|e|a|n email when job begins, ends, aborts, or no email
-q [queue_name] submit job to a specific queue
-pe (parallel environment: multi-core, multi-thread, multi-node)
-t n [-m:s]] (submit a job array)
```
