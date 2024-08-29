# Greenlight

## Gracefully shutdown

- `pgrep -l api` to get the process ID of api
- `pkill -SIGKILL api` which is not catchable and kills the app immediately

## Requests using Curl

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

## Binaries

- Check size of binaries `ls -l ./bin/name`
- Reduce binary `-ldflags='-s'` (Strip Symbol tabled and DWARF but is then harder to debug)
- List of dist: `go tool dist list` (set operating system eg.: `GOOS=linux GOARCH=amd64 go build {args}`)
- Location of go cache for better perf: `go env GOCACHE` and `go clean -cache` for cleaning cache
- Start binary: `./bin/api -db-dsn=postgres://...` (escape special characters like ?)

## Version Control

- check version number of binary: `./bin/api -version` (is the same as the git version number)

## DigitalOcean

### Connect to Droplet

- Connect to Droplet via `make production/connect`.

### Future changes to the droplet configuration

- Create a new bash: `remote/setup/02.sh`
- `rsync -rP --delete ./remote/setup greenlight@ip:~`
- `ssh -t greenlight@ip "sudo bash /home/greenlight/setup/02.sh"`

### Additional Information

- View logs of an bg service: `sudo journalctl -u api`
