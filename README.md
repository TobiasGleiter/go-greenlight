# Greenlight

## Gracefully shutdown

- `pgrep -l api` to get the process ID of api
- `pkill -SIGKILL api` which is not catchable and kills the app immediately

## Requests using sCurl

- `BODY='{"name": "Grace Smith", "email": "grace@example.com", "password": "invalid"}'`
- `curl -d "$BODY" localhost:4000/v1/users`

## Mirrors & Vendoring

### Mirrors

Where to look in the first place for the modules.

- `export GOPROXY=https://goproxy.io,https://proxy.golang.org,direct`; primary mirror is goproxy.io, fallback is proxy.golang.org
- `export GOPROXY=direct` disable module mirrors

### Vendoring

For complete ownership of the code.

- `go mod vendor` (creates folder called vendor and stores all necessary modules)
- `go clean -modcache` to check that the project runs without cached modules

Downsides: checked in packages and performance of CI/CD systems that clone the repository
