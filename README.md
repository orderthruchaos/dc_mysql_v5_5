# Getting Started

The MySQL 5.5.62 only has one available platform:  `linux/amd64`.  As such, do
not remove the `platform: linux/amd64` configuration from the compose file.

## Docker Desktop Setup for Mac OS X

If you are using Docker Desktop on Mac OS X, don't forget to enable the option

> "Use Rosetta for x86_64/amd64 emulation on Apple Silicon"

under "Virtual Machine Options".

You may need to install Rosetta 2 via the command line:

```bash
softwareupdate --install-rosetta
```

## Configuration

Be sure to open `docker-compose.yml` and change the username and passwords.

You may also wish to rename the Docker volume.

## Starting the Server

The usual startup command for `docker compose` should do:

```bash
docker compose up -d
```

## Using the Command Line Client

Unfortunately, the latest `mysql` CLI seems to hate this server.  You will
likely need to use `mysql` via the container itself.

If we use the `docker-compose.yml` file as-is, the command line to connect is:

```bash
mysql_user=my_user
docker compose exec -u root db mysql --user="$mysql_user" --password
```

The volumes are set up such that any files added to the local `./share/`
directory will be available under `/opt/share/` on the container.  For
example, the following commands:

```bash
touch share/foo.txt
docker compose exec -u root db ls -R '/opt'
```

will create the following output:

```bash
/opt:
share

/opt/share:
foo.txt
```

## Reference(s)

- [How to Create a MySql Instance with Docker Compose](https://medium.com/@chrischuck35/how-to-create-a-mysql-instance-with-docker-compose-1598f3cc1bee)
