# Greenlight

## Gracefully shutdown

- `pgrep -l api` to get the process ID of api
- `pkill -SIGKILL api` which is not catchable and kills the app immediately

## Requests using sCurl

- `BODY='{"name": "Grace Smith", "email": "grace@example.com", "password": "invalid"}'`
- `curl -d "$BODY" localhost:4000/v1/users`
