# Greenlight

## Gracefully shutdown

- `pgrep -l api` to get the process ID of api
- `pkill -SIGKILL api` which is not catchable and kills the app immediately
